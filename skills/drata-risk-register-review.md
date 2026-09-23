---
name: drata-risk-register-review
description: Review a Drata risk register — list risks, find the ones without a treatment plan or owner, and read register-level insights. Use when asked which risks need attention, which risks are untreated, or to produce a risk report.
api: Drata Public API v2
base_url: https://public-api.drata.com/public/v2
operations:
  - RiskRegisterPublicV2Controller_listRiskRegisters
  - RiskRegisterPublicV2Controller_getRiskRegister
  - RiskManagementPublicV2Controller_listRisks
  - RiskManagementPublicV2Controller_searchRisks
  - RiskManagementPublicV2Controller_searchRisksAcrossRegisters
  - RiskManagementPublicV2Controller_getRisk
  - RiskManagementPublicV2Controller_getRiskInsights
  - RiskManagementPublicV2Controller_updateRisk
generated: '2026-08-27'
method: generated
source: openapi/drata-api-v2-openapi.yml + conventions/drata-conventions.yml
---

# Review a Drata risk register

Read-first. The only write here is `updateRisk`, and only when the user explicitly asks for a change.

## Steps

1. **List registers** — `RiskRegisterPublicV2Controller_listRiskRegisters` (`GET /risk-registers`). Risks nest under `{riskRegisterId}`; you cannot address a risk without its register.

2. **Search across all registers** — `RiskManagementPublicV2Controller_searchRisksAcrossRegisters` (`GET /risks-search`) when the user's question spans the whole programme, or `RiskManagementPublicV2Controller_searchRisks` (`GET /risk-registers/{riskRegisterId}/risks-search`) when it is scoped to one register.

3. **List and read** — `RiskManagementPublicV2Controller_listRisks` then `getRisk`. Page with `cursor`; use `includeTotalCount` only when you actually need the total, it is opt-in for a reason.

4. **Read register insights** — `RiskManagementPublicV2Controller_getRiskInsights` (`GET /risk-registers/{riskRegisterId}/insights`) for the aggregate view rather than computing it yourself over pages.

5. **Report** risks with no treatment plan and no owner first; then by residual score.

## If asked to change a risk

- `RiskManagementPublicV2Controller_updateRisk` (`PUT /risk-registers/{riskRegisterId}/risks/{riskId}`) needs `update:risk`.
- Read the risk first, show the diff to the user, and apply only what they confirmed.
- **Never call `RiskManagementPublicV2Controller_deleteRisk` or `deleteRiskRegister` on your own initiative.** There is no restore path in this API and no recovery window is published. Deleting a register destroys every risk under it.

## Error handling

- **404** on a risk usually means the wrong `riskRegisterId`, not a missing risk — re-resolve the register.
- **403** means the caller's role or scopes are short: `read:risk`, `read:risk-registers`, `update:risk`.
- **412** — tenant has not accepted the API terms.
