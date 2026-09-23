---
name: drata-evidence-upload
description: Attach a piece of evidence (a file or an external artifact) to a Drata control or evidence-library item. Use when asked to upload evidence, refresh stale evidence, or push an artifact into Drata for an audit.
api: Drata Public API v2
base_url: https://public-api.drata.com/public/v2
operations:
  - UploadsPublicV2Controller_requestUploadUrl
  - EvidencePublicV2Controller_uploadArtifactFile
  - EvidencePublicV2Controller_createEvidence
  - EvidencePublicV2Controller_listEvidence
  - EvidencePublicV2Controller_getEvidence
  - EvidencePublicV2Controller_listEvidenceArtifacts
  - EvidencePublicV2Controller_updateEvidenceArtifact
  - EvidenceLibraryPublicV2Controller_listEvidenceLibrary
  - EvidenceLibraryPublicV2Controller_createEvidenceLibrary
generated: '2026-08-27'
method: generated
source: openapi/drata-api-v2-openapi.yml + conventions/drata-conventions.yml
---

# Upload evidence to Drata

This skill **writes**. Read the safety rules before the steps.

## Write safety

- Drata publishes **no idempotency-key mechanism**. A retried `POST` can create a duplicate evidence record. If a create times out or 5xx's, do **not** blindly retry: list the collection first and match on the natural key, then decide.
- Drata publishes **no restore, undo or unarchive operation** anywhere in the API, and no recovery window. `EvidencePublicV2Controller_deleteEvidence` and `deleteEvidenceArtifact` are terminal, and what they destroy is audit history. This skill never deletes; if the user asks you to, read the record, show it to them, and get an explicit confirmation first.
- Everything is workspace-scoped in the path. Confirm the `workspaceId` with the user before writing.

## Steps

1. **Find the target.** List evidence with `EvidencePublicV2Controller_listEvidence` (`GET /workspaces/{workspaceId}/evidence`) or the library with `EvidenceLibraryPublicV2Controller_listEvidenceLibrary`. Page with `cursor`.

2. **Get an upload URL for a file** — `UploadsPublicV2Controller_requestUploadUrl`
   `POST /upload-urls`. Use the returned URL to put the file.

3. **Upload the artifact file** — `EvidencePublicV2Controller_uploadArtifactFile`
   `POST /workspaces/{workspaceId}/evidence-files`.
   A **413** means the file exceeded Drata's size limit — compress or split rather than retrying identically.

4. **Create the evidence record** — `EvidencePublicV2Controller_createEvidence`
   `POST /workspaces/{workspaceId}/evidence`. Requires `create:evidence` scope.

5. **Verify** — `EvidencePublicV2Controller_getEvidence` and `EvidencePublicV2Controller_listEvidenceArtifacts`. Confirm the artifact is attached before reporting success. Never report success from the create response alone; verify by read-back, because there is no idempotency guard behind you.

## Error handling

- **400** — schema/validation failure; the message names the field.
- **412** — tenant has not accepted the API terms. Human escalation.
- **413** — file too large.
- **422** — semantically unprocessable; the message states what to disambiguate.
- **503** — a third-party system Drata depends on was unavailable; retry with backoff.
