# Failure Investigation (Reference)

**Owner:** `web-api-and-integration-testing`. Use this sequence when an issue occurs.

## Investigation Sequence

1. **Establish expected behavior** — the expected business outcome.
2. **Observe the UI** — record exactly what the customer sees.
3. **Inspect the network request** — was a request sent? to the expected endpoint? was it valid?
4. **Inspect the API response** — status · body · error · business result.
5. **Check persistence** — was the expected data stored?
6. **Check integration** — did downstream processing occur?
7. **Correlate logs** — use request/correlation identifiers.
8. **Compare working vs failing** — change one meaningful condition at a time.
9. **Report the narrowest confirmed failure** — do not claim a root cause without evidence.

> Prefer: "The checkout UI receives HTTP 500 from the order API after payment authorization."
> Over: "The payment integration is broken." — unless payment is proven to be the cause.

## Performance Considerations

When performance is in scope, verify defined expectations for page loading · API response time · throughput · concurrency · third-party latency · database performance. Do not invent thresholds — use documented SLAs. Tools (authorized test env): JMeter · k6 · Gatling. Do not run substantial load against production or third-party services without authorization.

## Security Considerations

Within authorized scope consider: authentication · authorization · object-level access control · input validation · sensitive-data exposure · security headers · session handling · cookies · CORS · rate limiting. Align with OWASP Web Security Testing Guide, OWASP Top 10, OWASP API Security Top 10. Stay within the authorized environment and scope.

## eCommerce Flows

- **Product:** type · options · availability · price · special price · inventory · quantity rules.
- **Cart:** add · update · remove · quantity · coupon · promotion · free gift · cart total · persistence.
- **Wishlist:** guest/logged-in behavior · authentication transition · addition · removal · counter · persistence.
- **Checkout:** guest/logged-in · address · shipping · store pickup · tax · promotions · payment · review · submission.
- **Payment:** success · decline · failure · timeout · retry · duplicate submission · cancellation · authentication challenges (3-D Secure via provider test scenarios) · final transaction state.
- **Order:** creation · number · customer · items · quantity · price · discount · tax · shipping · total · payment status · fulfilment info.
- **Post-order:** invoice · shipment · cancellation · refund · credit memo · notification.

Canonical checklist and cross-system chain: `shared/ecommerce-coverage.md`.
