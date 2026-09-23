---
name: drata-audit-readiness-report
description: Produce a read-only audit-readiness report for a Drata workspace — which controls are not ready, which monitoring tests are failing, and which framework requirements are uncovered. Use when someone asks how ready they are for a SOC 2, ISO 27001 or other framework audit.
api: Drata Public API v2
base_url: https://public-api.drata.com/public/v2
operations:
  - FrameworksPublicV2Controller_getFrameworks
  - FrameworksPublicV2Controller_listFrameworkRequirements
  - FrameworksPublicV2Controller_listFrameworkRequirementControls
  - ControlsPublicV2Controller_getControls
  - ControlsPublicV2Controller_getControlById
  - ControlsPublicV2Controller_getMappedRequirements
  - MonitorsPublicV2Controller_listMonitors
  - MonitorsPublicV2Controller_listMonitorTestFailures
generated: '2026-08-27'
method: generated
source: openapi/drata-api-v2-openapi.yml + conventions/drata-conventions.yml
---

# Audit readiness report

Read-only. Every operation in this skill is a GET; nothing here writes to Drata.

## Before you start

- Authenticate with `Authorization: Bearer <DRATA_API_KEY>`. The key is a long-lived API key, not a JWT.
- Almost everything below is workspace-scoped in the path. Resolve the workspace first and carry `workspaceId` through the whole run — the same id in a different workspace returns 404.
- Rate limit is **500 requests/minute per source IP**, not per key. Adding keys does not add throughput. On 429, honour `Retry-After`.

## Steps

1. **List frameworks in the workspace** — `FrameworksPublicV2Controller_getFrameworks`
   `GET /workspaces/{workspaceId}/frameworks`. Pick the framework the user named (SOC 2, ISO 27001, HIPAA, PCI DSS…).

2. **Pull the requirements for that framework** — `FrameworksPublicV2Controller_listFrameworkRequirements`
   `GET /workspaces/{workspaceId}/frameworks/{frameworkId}/requirements`. Page with `cursor`; stop when the response returns no `pagination.cursor`.

3. **For each requirement, find the controls mapped to it** — `FrameworksPublicV2Controller_listFrameworkRequirementControls`
   `GET /workspaces/{workspaceId}/frameworks/{frameworkId}/requirements/{requirementId}/controls`.
   A requirement with an empty control list is an **uncovered requirement** — report it first, it is the finding an auditor opens with.

4. **List controls and their readiness** — `ControlsPublicV2Controller_getControls`
   `GET /workspaces/{workspaceId}/controls`. Use `expand[]` to pull related objects in one call instead of N follow-ups; read the operation's own `expand[]` enum rather than assuming a global vocabulary.

5. **List monitoring tests and their failures** — `MonitorsPublicV2Controller_listMonitors`, then `MonitorsPublicV2Controller_listMonitorTestFailures`
   `GET /workspaces/{workspaceId}/monitoring-tests` and `GET /workspaces/{workspaceId}/monitoring-tests/{testId}/failures`.
   Failing tests are the live evidence gap; group them by the control they back.

6. **Report** three sections, in this order: uncovered requirements, controls that are not ready, failing monitoring tests. Cite the framework name and the workspace in the header.

## Error handling

- **412** — the tenant has not accepted the Drata API terms and conditions. Every operation returns this until a Drata administrator accepts them in the app. Escalate to a human; do not retry.
- **402** — the tenant's plan does not include this feature. Widening key scopes will never clear it.
- **403** — the API key lacks the scope. `read:controls`, `read:framework`, `read:monitor-test` are the ones this skill needs.
- **429** — rate limited. Back off, honour `Retry-After`, resume.
- Error bodies are `{name, statusCode, message, code, debugInfo?}`. The `code` member is a Drata-internal number with no public registry — quote it verbatim when escalating, do not try to interpret it.
