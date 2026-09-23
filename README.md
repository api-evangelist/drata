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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
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
- Risk Management
- Trust Center
- Audit
- Vendor Risk Management
- Compliance Automation

## Timestamps

- **Created:** 2026-05-08
- **Modified:** 2026-08-27

## APIs

### Drata Public API v2

Drata's Public REST API v2 — 197 operations across 132 paths covering assets, audits, audit requests, background checks, company, control library, controls, control notes/owners, custom connections, custom data records, custom field definitions, devices and device documents, events, evidence and the evidence library, frameworks, groups, HRIS user identities, monitoring tests, personnel, policies and policy languages, risks, risk registers, risk library, risk notes and documents, tasks, uploads, user documents, user-assigned policies, users and roles, vendors, vendor documents, vendor security reviews, vendor types, and workspaces. Bearer API-key auth, cursor pagination, and an `expand[]` query parameter for related objects. Regional bases exist for US, EU and APAC.

- **Human URL:** [https://developers.drata.com/openapi/reference/v2/overview/](https://developers.drata.com/openapi/reference/v2/overview/)
- **Base URL:** `https://public-api.drata.com/public/v2`

#### Tags

- GRC
- Compliance
- REST

#### Properties

- [OpenAPI](openapi/drata-api-v2-openapi.yml)
- [Documentation](https://developers.drata.com/openapi/reference/v2/overview/)
- [APIReference](https://developers.drata.com/openapi/reference/v2/overview/)
- [GettingStarted](https://developers.drata.com/developer-portal/v2/recipes/create-an-api-key/)
- [Authentication](authentication/drata-authentication.yml)
- [Overlay](overlays/drata-api-v2-overlay.yaml)

### Drata Custom Connections API

Build custom integrations to automate evidence collection from any internal or third-party system.

- **Human URL:** [https://developers.drata.com/openapi/reference/v2/tag/Custom-Connections/](https://developers.drata.com/openapi/reference/v2/tag/Custom-Connections/)
- **Base URL:** `https://public-api.drata.com/public/v2`

#### Tags

- GRC
- Integration
- Evidence

#### Properties

- [Documentation](https://developers.drata.com/openapi/reference/v2/tag/Custom-Connections/)
- [GettingStarted](https://developers.drata.com/developer-portal/v2/recipes/custom-connections/)
- [OpenAPI](openapi/drata-api-v2-openapi.yml)

### SafeBase Trust API

SafeBase Trust API — 41 operations for trust centers, security questionnaires, NDA settings, document libraries, knowledge-base entries, access requests and trust-center updates. SafeBase was acquired by Drata in 2024 and the API remains published on the safebase.io domain; the spec declares servers https://app.safebase.io/api/ext/v1/rest and contact support@safebase.io. Authenticated with an `x-sb-api-key` header.

- **Human URL:** [https://docs.safebase.io/reference/getaccounts](https://docs.safebase.io/reference/getaccounts)
- **Base URL:** `https://app.safebase.io/api/ext/v1/rest`

#### Tags

- Trust Center
- Questionnaires
- Security

#### Properties

- [OpenAPI](openapi/drata-safebase-trust-api-openapi.yml)
- [Documentation](https://docs.safebase.io/reference/getaccounts)
- [APIReference](https://docs.safebase.io/reference/getaccounts)

### Drata MCP Server

Drata's hosted remote Model Context Protocol server (Beta). MCP-compatible clients (Claude, ChatGPT, Cursor, Microsoft Copilot) connect over OAuth 2.1 with PKCE to regional endpoints for the US, EU and APAC, and read live compliance data — controls, policies, monitoring tests, risks, risk registers, workspaces and assigned policies — bounded by the intersection of the granted OAuth scopes and the user's Drata role.

- **Human URL:** [https://developers.drata.com/developer-portal/v2/recipes/mcp-oauth-setup/](https://developers.drata.com/developer-portal/v2/recipes/mcp-oauth-setup/)
- **Base URL:** `https://mcp.drata.com/mcp/`

#### Tags

- MCP
- Artificial Intelligence
- Compliance

#### Properties

- [MCPServer](mcp/drata-mcp.yml)
- [ToolCrosswalk](mcp/drata-tool-crosswalk.yml)
- [Documentation](https://developers.drata.com/developer-portal/v2/recipes/mcp-oauth-setup/)
- [OAuthScopes](scopes/drata-scopes.yml)
- [Blog](https://drata.com/blog/introducing-mcp-built-for-ai)

## Common Properties

- [AgenticAccess](agentic-access/drata-agentic-access.yml)
- [TrustCenter](security/drata-trust-center.yml)
- [VulnerabilityDisclosure](security/drata-vulnerability-disclosure.yml)
- [DomainSecurity](security/drata-domain-security.yml)
- [Authentication](authentication/drata-authentication.yml)
- [GitHubOrganization](https://github.com/drata)
- [LinkedIn](https://www.linkedin.com/company/drata)
- [Website](https://drata.com/)
- [Developer](https://developers.drata.com/)
- [Plans](plans/drata-plans-pricing.yml)
- [RateLimits](rate-limits/drata-rate-limits.yml)
- [FinOps](finops/drata-finops.yml)
- [MCPServer](mcp/drata-mcp.yml)
- [ToolCrosswalk](mcp/drata-tool-crosswalk.yml)
- [OAuthScopes](scopes/drata-scopes.yml)
- [WellKnown](well-known/drata-well-known.yml)
- [Conventions](conventions/drata-conventions.yml)
- [ErrorCatalog](errors/drata-problem-types.yml)
- [Lifecycle](lifecycle/drata-lifecycle.yml)
- [ChangeLog](changelog/drata-changelog.yml)
- [Conformance](conformance/drata-conformance.yml)
- [DataModel](data-model/drata-data-model.yml)
- [Packages](packages/drata-packages.yml)
- [LLMsTxt](llms/drata-llms.txt)
- [Overlay](overlays/drata-api-v2-overlay.yaml)
- [Examples](examples/drata-examples.yml)
- [Drata Agent Skills](skills/_index.yml)
- [StatusPage](https://status.drata.com/)
- [Security](security/drata-vulnerability-disclosure.yml)
- [Compliance](https://trust.drata.com/)
- [DeveloperPortal](https://developers.drata.com/)
- [Documentation](https://developers.drata.com/openapi/reference/v2/overview/)
- [APIReference](https://developers.drata.com/openapi/reference/v2/overview/)
- [GettingStarted](https://developers.drata.com/developer-portal/v2/recipes/create-an-api-key/)
- [Support](https://help.drata.com/)
- [Blog](https://drata.com/blog)
- [Pricing](https://drata.com/pricing)
- [SignUp](https://drata.com/demo)
- [Login](https://app.drata.com/)
- [TermsOfService](https://drata.com/terms)
- [PrivacyPolicy](https://drata.com/privacy)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
