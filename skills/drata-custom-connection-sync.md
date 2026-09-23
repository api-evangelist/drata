---
name: drata-custom-connection-sync
description: Push data from an external system into Drata as compliance evidence using a Custom Connection — create the connection with a JSON Schema, then sync records directly or as an atomic session batch. Use when asked to get data from an internal tool into Drata.
api: Drata Public API v2
base_url: https://public-api.drata.com/public/v2
operations:
  - CustomConnectionsPublicV2Controller_listCustomConnections
  - CustomConnectionsPublicV2Controller_createCustomConnection
  - CustomConnectionsPublicV2Controller_getCustomConnection
  - CustomConnectionsPublicV2Controller_updateCustomConnection
  - CustomDataRecordsPublicV2Controller_listCustomDataRecords
  - CustomDataRecordsPublicV2Controller_createCustomData
  - CustomDataRecordsPublicV2Controller_updateCustomData
  - CustomDataRecordsPublicV2Controller_listSessions
  - CustomDataRecordsPublicV2Controller_uploadSessionRecords
  - CustomDataRecordsPublicV2Controller_performSessionAction
generated: '2026-08-27'
method: generated
source: >-
  openapi/drata-api-v2-openapi.yml +
  https://developers.drata.com/developer-portal/v2/recipes/custom-connections/
---

# Sync an external system into Drata

## Choose the provider type first

Drata's Custom Connections take three provider types, and the type decides the whole shape of the integration:

| Provider type | Schema required? | Record endpoint |
|---|---|---|
| `CUSTOM` | Yes — supply `schema` (JSON Schema) **or** `sampleData` plus `displayNameKey` | `/custom-connections/{connectionId}/resources/{resourceId}/records` |
| `MDM` | No — Drata's fixed common device model | `/custom-connections/{connectionId}/devices` |
| `HRIS` | No — Drata's fixed common HRIS model | `/custom-connections/{connectionId}/hris-user-identities` |

Passing `schema`, `sampleData`, `displayNameKey` or `workspaceIds` on an `MDM` or `HRIS` connection returns **400 Bad Request**. Sessions and record management below apply to `CUSTOM` connections only.

## Steps

1. **Check for an existing connection** — `listCustomConnections` (`GET /custom-connections`). Re-use rather than creating a duplicate; there is no idempotency key to protect you.

2. **Create the connection** — `createCustomConnection` (`POST /custom-connections`) with `name`, `providerTypes`, `workspaceIds`, and for `CUSTOM` either a JSON Schema in `schema` or a representative record in `sampleData` (not both) plus a `displayNameKey` that is a top-level key of the schema.

3. **Sync records.** Two modes, and the choice matters:
   - **Direct upload** — `createCustomData` (`POST .../records`). Immediately live. Right for incremental single-record updates.
   - **Session batch** — `listSessions`, then `uploadSessionRecords` (`POST .../sessions/{sessionId}`), then `performSessionAction` to complete. Drata **atomically replaces the active dataset** with the batch on completion. Use this for full syncs: it is the only all-or-nothing path, and it is the closest thing this API has to a transaction.

4. **Verify** — `listCustomDataRecords` to confirm the records landed.

## Write safety

- Completing a session **replaces** the active dataset. A partial batch completed by mistake silently drops every record you left out. Assemble the whole batch before calling the completion action.
- `deleteCustomData` and `deleteCustomConnection` have no restore path in this API. Deleting a connection orphans the evidence built on it.
- No idempotency keys: a retried record create can duplicate. List and match before retrying.

## Error handling

- **400** — most often a field sent to the wrong provider type (see the table above), or a `displayNameKey` that is not a top-level schema key.
- **412** — tenant has not accepted the API terms.
- **429** — 500 req/min per source IP. Bulk syncs hit this: throttle and use session batches rather than thousands of single-record POSTs.
