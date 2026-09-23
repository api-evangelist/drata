---
name: drata-vendor-security-review
description: Run third-party/vendor risk work in Drata — list vendors, open a security review, send a security questionnaire, and track review actions. Use when asked about vendor risk, a new vendor assessment, or outstanding questionnaires.
api: Drata Public API v2
base_url: https://public-api.drata.com/public/v2
operations:
  - VendorsPublicV2Controller_listVendors
  - VendorsPublicV2Controller_getVendor
  - VendorsPublicV2Controller_getVendorStats
  - VendorsPublicV2Controller_createVendor
  - VendorsPublicV2Controller_listVendorQuestionnaires
  - VendorsPublicV2Controller_sendQuestionnaireToVendor
  - VendorSecurityReviewsPublicV2Controller_listVendorSecurityReviewsAcrossVendors
  - VendorSecurityReviewsPublicV2Controller_listVendorSecurityReviews
  - VendorSecurityReviewsPublicV2Controller_createVendorSecurityReview
  - VendorSecurityReviewsPublicV2Controller_createVendorSecurityReviewWithFile
  - VendorSecurityReviewsPublicV2Controller_getVendorSecurityReview
  - VendorSecurityReviewsPublicV2Controller_sendSecurityQuestionnaire
  - VendorSecurityReviewsPublicV2Controller_listSecurityReviewActions
  - VendorSecurityReviewsPublicV2Controller_performSecurityReviewAction
generated: '2026-08-27'
method: generated
source: openapi/drata-api-v2-openapi.yml + conventions/drata-conventions.yml
---

# Vendor security review

## Read path

1. **Portfolio view** — `VendorsPublicV2Controller_getVendorStats` (`GET /vendors-stats`) for the aggregate, then `listVendors` (`GET /vendors`) with `cursor` paging.
2. **Reviews across the whole book** — `VendorSecurityReviewsPublicV2Controller_listVendorSecurityReviewsAcrossVendors` (`GET /vendor-security-reviews`). Use this rather than looping `listVendorSecurityReviews` per vendor; it is one paged call instead of N.
3. **Outstanding questionnaires** — `VendorsPublicV2Controller_listVendorQuestionnaires` (`GET /vendors/{vendorId}/questionnaires`).

## Write path

These operations send mail to third parties. Confirm with the user before every one of them.

4. **Open a review** — `createVendorSecurityReview` (`POST /vendors/{vendorId}/security-reviews`), or `createVendorSecurityReviewWithFile` when attaching the vendor's report in the same call.
5. **Send a questionnaire** — `sendSecurityQuestionnaire` (`POST /vendors/{vendorId}/security-questionnaires`) or `sendSecurityQuestionnaireForSecurityReview` to attach it to an existing review.
   **This emails a real person at the vendor.** There is no idempotency key on this API, so a blind retry can send a second questionnaire. If the call times out, list questionnaires and check before resending.
6. **Progress a review** — `listSecurityReviewActions` then `performSecurityReviewAction` (`POST /vendors/{vendorId}/security-reviews/{securityReviewId}/actions`). Read the available actions first rather than guessing an action name.

## Related surface

The SafeBase Trust API (`openapi/drata-safebase-trust-api-openapi.yml`, base `https://app.safebase.io/api/ext/v1/rest`) is the other half of this workflow — it is where *inbound* questionnaires and the trust centre live, and it authenticates with a different credential (`x-sb-api-key`), not the Drata bearer key.

## Error handling

- **409** — a business-rule conflict, e.g. a review already open for that vendor. Re-read before retrying.
- **402** — vendor security reviews are not in the tenant's plan.
- **412** — tenant has not accepted the API terms.
- `VendorsPublicV2Controller_deleteVendor` is terminal with no restore path. Do not call it without explicit confirmation.
