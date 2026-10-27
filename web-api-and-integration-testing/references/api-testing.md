# API Testing (Reference)

**Owner:** `web-api-and-integration-testing`.

## Endpoint and Method Validation

Validate supported operations: GET · POST · PUT · PATCH · DELETE. Confirm unsupported methods are handled correctly when relevant to the contract.

## Status Codes

Validate according to the actual contract. Common semantics: `200` `201` `202` `204` `400` `401` `403` `404` `409` `422` `429` `500` `502` `503`. Do not assert a code purely because it is common practice — the specification is the source of truth.

## Request Validation

Required · optional · conditionally required · unknown · read-only fields · null · empty string · whitespace · boolean · integer · decimal · date · date/time · array · nested object · max/min length · range · enum · special characters · Unicode · malformed JSON.

## Response Validation

HTTP status · Content-Type · schema · required fields · field type · field format · business values · error structure · pagination metadata · sensitive information · response time where a requirement exists.

## Headers

Authorization · Content-Type · Accept · Cache-Control · Location · Retry-After · correlation/request IDs. Security headers: Strict-Transport-Security · Content-Security-Policy · X-Content-Type-Options · Referrer-Policy. Validate the exact requirement, not a blanket assumption.

## Authentication

No credentials · valid · invalid · expired token · revoked token · malformed token · missing token · incorrect scheme. Verify the system rejects invalid authentication safely. Do not record usable credentials/tokens in shared evidence.

## Authorization

Authentication asks "who is the caller?"; authorization asks "is this caller allowed to do this to this resource?" Test: own resource · another user's resource · lower role accessing privileged operation · direct resource access · modified object/customer/order ID · restricted field update · restricted method. Watch **IDOR/BOLA**. Do not exploit production.

## Business Rule Testing

A syntactically valid request can violate a rule. Validate state restrictions · quantity rules · pricing · availability · eligibility · promotion/shipping eligibility · payment restrictions · order-state transitions.

> `200 OK` is not sufficient if the API accepts a quantity above the allowed maximum.

## Pagination, Sorting, Filtering, Search

- **Pagination:** first/middle/final page · beyond result set · min/max page size · empty result · total count; check for missing/duplicate records across pages.
- **Sorting:** asc/desc · numeric · alphabetical · date/time · nulls.
- **Filtering:** one · multiple · unsupported · empty result · boundaries.
- **Search:** exact · partial · case sensitivity · special characters · no result.

Follow the API contract.

## Idempotency and Duplicate Submission

Test where duplicates create risk (payment, order creation, refund, customer, coupon, inventory). Consider: same request twice · repeated click · retry after timeout · same/different idempotency key. A retry must not create two orders when the operation is meant to run once.

## Concurrency

Simultaneous operations: two inventory updates · multiple checkout submissions · concurrent cart updates · parallel order modification · multiple refunds. Validate data consistency · locking · conflict handling · duplicate prevention · final persisted state. No load/destructive testing without authorization.

## Error Handling

Check: correct status class · consistent schema · meaningful error identifier · safe message · correlation ID. Watch for exposure of stack traces, DB details, file paths, internal hostnames, secrets, tokens, customer data.

## Contract Testing

Validate provider/consumer compatibility: field existence · type · required/optional rules · enum values · nested structures · backward compatibility. Failures: required field removed · type changed · enum changed · meaning changed · optional became mandatory. Recommend automated contract checks when regressions recur.

## Postman Guidelines

Organize requests by API/domain · use environment variables for non-sensitive config · protect secrets · validate response behavior (not just status) · include schema/field-level assertions · validate business rules · keep assertions readable.

```javascript
pm.test("HSTS header is present", function () {
  pm.expect(pm.response.headers.get("Strict-Transport-Security")).to.exist;
});

pm.test("returns the discounted total", function () {
  const body = pm.response.json();
  pm.expect(body.discount).to.eql(12);
  pm.expect(body.total).to.eql(108);
});
```
