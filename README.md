# Drata (drata)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Drata is a continuous security and compliance automation platform supporting SOC 2, ISO 27001, HIPAA, PCI DSS, GDPR, and more, with policies, evidence, and trust center. Drata exposes a public REST API plus the SafeBase Trust API (acquired) and a Custom Connections framework for evidence collection.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/drata/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/drata/refs/heads/main/apis.yml)

## Tags

- GRC
- Compliance
- SOC 2
- ISO 27001
- Security

## Timestamps

- **Created:** 2026-05-08
- **Modified:** 2026-05-08

## APIs

### Drata Public API v2

Public REST API for managing controls, frameworks, evidence, personnel, assets, policies, and tests. v2 expands endpoints and improves data structures over v1.

- **Human URL:** [https://developers.drata.com/openapi/reference/v2/overview/](https://developers.drata.com/openapi/reference/v2/overview/)
- **Base URL:** `https://public-api.drata.com`

#### Tags

- GRC
- Compliance
- REST

#### Properties

- [Documentation](https://developers.drata.com/openapi/reference/v2/overview/)
- [Authentication](https://developers.drata.com/openapi/reference/v2/overview/)
- [Postman Collection](collections/drata.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/drata.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Drata Custom Connections API

Build custom integrations to automate evidence collection from any internal or third-party system.

- **Human URL:** [https://developers.drata.com/openapi/reference/v2/tag/Custom-Connections/](https://developers.drata.com/openapi/reference/v2/tag/Custom-Connections/)
- **Base URL:** `https://public-api.drata.com`

#### Tags

- GRC
- Integrations
- Evidence

#### Properties

- [Documentation](https://developers.drata.com/openapi/reference/v2/tag/Custom-Connections/)
- [Postman Collection](collections/drata.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/drata.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### SafeBase Trust API

Manage SafeBase trust centers and security questionnaires programmatically; acquired by Drata and now part of the Drata platform.

- **Human URL:** [https://docs.safebase.io/reference/getaccounts](https://docs.safebase.io/reference/getaccounts)
- **Base URL:** `https://api.safebase.io`

#### Tags

- Trust Center
- Questionnaires
- Security

#### Properties

- [Documentation](https://docs.safebase.io/reference/getaccounts)
- [Postman Collection](collections/drata.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/drata.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Drata MCP Server

Model Context Protocol server enabling AI agents to interact with Drata for compliance workflows.

- **Human URL:** [https://drata.com/blog/drata-mcp-built-for-ai-native-trust-management](https://drata.com/blog/drata-mcp-built-for-ai-native-trust-management)

#### Tags

- MCP
- AI
- Compliance

#### Properties

- [Blog](https://drata.com/blog/drata-mcp-built-for-ai-native-trust-management)
- [Postman Collection](collections/drata.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/drata.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/drata)
- [LinkedIn](https://www.linkedin.com/company/drata)
- [Website](https://drata.com/)
- [Developer](https://developers.drata.com/)
- [Plans](plans/drata-plans-pricing.yml)
- [Rate Limits](rate-limits/drata-rate-limits.yml)
- [Fin Ops](finops/drata-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
