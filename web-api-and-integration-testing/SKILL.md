---
name: web-api-and-integration-testing
description: >
  Designs, executes, reviews, and troubleshoots testing across web applications,
  REST APIs, backend services, and integrated systems. Use this skill when
  validating UI behavior, API contracts, authentication and authorization,
  request and response data, data persistence, third-party integrations,
  asynchronous processing, failure and retry behavior, or end-to-end workflows
  spanning multiple system boundaries.
metadata:
  version: 2.0.0
  owner: QA Practice
  tags: [api-testing, integration, ui-testing, e2e, auth]
---

# Web, API, and Integration Testing

## Purpose

Validate user-facing behavior, service contracts, data exchange, persistence, and end-to-end business outcomes across web applications, APIs, backend services, and integrated systems.

Success means: the user gets correct behavior · the correct request is sent · the API enforces its contract and business rules · data is mapped and persisted correctly · downstream systems receive the right information · failures are handled safely · auth/authz behave correctly · the final business outcome is correct.

## When to Use

Use when asked to: test a web app · test a REST API · create/validate/review API scenarios · test frontend↔backend communication · test auth or authz · validate methods/status codes/headers/payloads · verify request/response schemas · investigate network requests or console errors · test third-party integrations · test async processing (queues, events, webhooks, jobs) · validate data synchronization · verify UI/API/DB consistency · test retries, timeouts, dependency failures · investigate integration defects · test an end-to-end workflow · verify an eCommerce integration · validate API security behavior · prepare Postman tests · assess regression impact across UI/API/integrations.

## When NOT to Use

| Situation | Use instead |
|---|---|
| Designing the test cases (not executing them) | `test-case-design-and-management` |
| Building/maintaining the automated suite | `test-automation-and-frameworks` |
| A failure is confirmed and needs root-cause analysis | `defect-management-and-root-cause-analysis` |
| Planning scope, strategy, or release gates | `test-strategy-and-planning` |

## Operating Principles

1. Never treat HTTP 2xx alone as a pass — verify the business outcome.
2. Correct UI ≠ correct backend data; correct API data ≠ correct UI usage.
3. Validate authorization independently from authentication.
4. Separate transport success from business success.
5. Verify persisted data when persistence is part of the outcome.
6. Verify downstream effects when integrations are involved.
7. Treat async operations differently from sync ones; do not immediately flag time-dependent async behavior as a defect.
8. Test duplicate/repeated actions when they create financial or data-integrity risk.
9. Never expose secrets or sensitive customer data in evidence.
10. Do not perform destructive, intrusive, security, or load-heavy testing without authorization.
11. Separate confirmed observations from diagnostic hypotheses.

## System Journey Mapping

Identify participating layers first. Typical:

```
User → Browser UI → Frontend → API Gateway → Backend → Database → Integration → External System → Response/Event → UI
```

eCommerce: `Product → Cart → Checkout → Payment → Order → Inventory → Fulfilment → Confirmation`.

| Layer | Component | Input | Expected output | Evidence |
|---|---|---|---|---|
| UI | Frontend | User action | Correct request triggered | Browser network |
| API | Backend | Request | Correct response / business rule | API response |
| Data | Persistence | Processed data | Correct stored state | DB / API |
| Integration | External service | Mapped request | Correct downstream processing | Logs / response |
| UI | Frontend | Final state | Correct customer outcome | Screenshot / UI |

## Workflow

1. **Understand the business journey** — actor, entry point, preconditions, inputs, rules, expected and failure outcomes, systems, integrations, persistence, async.
2. **Identify interfaces and boundaries** — for each: input, output, contract, ownership, auth/authz, timeout, retry, error behavior, data ownership.
3. **Establish expected behavior** — requirements, acceptance criteria, OpenAPI/Swagger, architecture docs, business rules, designs, existing behavior, contracts. Separate confirmed / assumed / unknown; never invent contracts.
4. **Prepare environment and data** — env, version, base URL, auth method, accounts, roles, data, integration config, flags, sandbox, DB state, queue config. Never expose credentials or PII.
5. **Execute the happy path** — verify across UI, request, API response, persistence, integration, and final business result; do not stop at the first successful layer.
6. **Test negative and boundary behavior** — missing/empty/null/invalid type/format, below-min/max/above-max, unsupported enum, malformed request, unknown resource, duplicate submission, unauthorized/forbidden, expired auth, invalid transition. Select by risk, not mechanically.
7. **Validate failure handling** — dependency down, timeout, network interruption, invalid/partial response, retry, duplicate, delayed/missing/out-of-order event, partial completion. Check both technical handling and customer-visible behavior.
8. **Verify persistence and downstream effects** — API GET, DB query, admin UI, downstream system, queue/event, order record, logs. Never rely on UI confirmation alone for transactions.
9. **Correlate evidence** — timestamps and request/correlation/trace/order/transaction/message IDs; use the minimum identifying info, sanitize before sharing.
10. **Record findings** — expected vs actual, repro, environment, data, request, response, timestamp, correlation ID, business impact; distinguish observation from suspected root cause.

## At-a-Glance Rules

- **Status codes:** validate against the actual contract, not common practice. The spec is the source of truth.
- **Auth vs authz:** authz = "is this caller allowed to do this to this resource?" — watch IDOR/BOLA. Do not exploit production.
- **Business rules:** a syntactically valid request can still violate a rule (e.g. quantity above maximum returning `200 OK`).
- **Idempotency:** retries must not create duplicate business transactions (payment, order, refund, coupon, inventory).
- **Async:** account for eventual consistency; do not flag permitted temporary states.
- **Timeout:** ask "did the remote system still process the transaction?" — critical for payment/order.

## Default Output Structure

1. Journey/Scope · 2. Interfaces and Boundaries · 3. Expected Behavior (confirmed/assumed) · 4. Environment and Data · 5. Test Scenarios (UI/API/Integration/E2E) · 6. Failure-Handling Coverage · 7. Persistence & Downstream Verification · 8. Evidence · 9. Findings & Gaps.

## References

- `shared/ecommerce-coverage.md` — eCommerce coverage and cross-system chain
- `shared/evidence-templates.md` — evidence capture and sanitization
- `shared/severity-and-priority.md` — severity/priority model
- `references/ui-testing.md` — web UI, responsive, compatibility, accessibility, DevTools
- `references/api-testing.md` — endpoints, status codes, request/response, headers, pagination, contract, Postman
- `references/integration-testing.md` — mapping, sync/async, retry, timeout, partial failure, reconciliation
- `references/failure-investigation.md` — investigation sequence, eCommerce flows, performance/security
- `references/example-api-suite.md` — a worked API/integration example
