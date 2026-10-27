# Coverage Dimensions (Reference)

Full catalogue of coverage dimensions. Apply only those relevant to the feature and its risk.

**Owner:** `test-case-design-and-management`.

## Input Coverage

Valid · invalid · empty · missing · null · minimum · maximum · below-minimum · above-maximum · malformed · unsupported format · leading/trailing spaces · special characters · Unicode · duplicate values · very large values · decimal and rounding behavior.

## User and Permission Coverage

Guest · authenticated · different customer groups · administrator · restricted role · unauthorized · expired session · disabled/locked account · direct-access attempts without permission.

## State and Interaction Coverage

Initial state · valid transition · invalid transition · repeated action · double submission · refresh · back navigation · session expiration · concurrent update · interrupted process · recovery after failure.

## Integration Coverage

Successful request/response · invalid request · invalid response · missing fields · partial response · timeout · network failure · retry · duplicate message · delayed/asynchronous processing · out-of-order response · authentication failure · authorization failure · rate limiting · downstream unavailability · data mismatch.

## Data Coverage

Create · read · update · delete · persistence · mapping · calculations · rounding · sorting · filtering · search · pagination · export · import · time zone · date format · currency · localization · duplicate prevention · referential integrity.

## UI and Compatibility Coverage

Supported browsers · devices · responsive viewports · orientation · keyboard navigation · focus order · screen-reader labels · color contrast · zoom/text scaling · loading indicators · empty states · error messages · long content · large prices/quantities · missing images · slow network.

## eCommerce Coverage

See `shared/ecommerce-coverage.md` — the canonical checklist (customer, catalog, cart, wishlist, checkout, payment, order, post-order, integrations, cross-system chain).

## Non-Functional (when risk indicates)

Accessibility (WCAG when required) · performance (response time, throughput, concurrency) · security (authentication, authorization, input validation, sensitive-data exposure) · compatibility.
