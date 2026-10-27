# Evidence Templates and Sanitization (Shared Reference)

Canonical evidence capture formats and the sanitization rules every skill must respect.

**Owned by:** `defect-management-and-root-cause-analysis`.
**Linked from:** `web-api-and-integration-testing`, `test-case-design-and-management`, `test-strategy-and-planning`.

## Sanitization Rules (non-negotiable)

Never include in shared evidence:

- Passwords, access/refresh tokens, session IDs, API keys
- Payment credentials, private certificates
- Personally identifiable information (PII) beyond what is strictly required

Also prevent secrets appearing in logs, screenshots, traces, reports, or source control.

## Evidence Types

| Type | Examples |
|---|---|
| **UI** | Screenshot, screen recording, console error, network request, visible error message, rendered/DOM state. |
| **API** | Method, endpoint, headers (safe), request/response body, status, timing, correlation ID. |
| **Server / app** | Application logs, web/integration logs, error traces, queue state, job state, alerts, trace IDs. |
| **Data** | Database state, order/product/inventory/customer state, configuration values (where authorized). |
| **Environment** | App version, deployment version, browser/device, feature flags, cache/CDN/WAF config, integration availability. |

Evidence should **support a conclusion**, not merely increase attachment count.

## Request / Response Evidence Template

**Environment**
- Environment:
- Build/version:
- Browser/device:
- Account type:

**Request**
- Method:
- Endpoint:
- Relevant headers:
- Sanitized body:
- Timestamp:
- Request/Correlation ID:

**Response**
- Status:
- Relevant headers:
- Sanitized body:
- Response time (when relevant):

**Business Result**
- UI result:
- Persisted data:
- Downstream result:

**Attachments**
- Screenshot / console / network / log / database-or-admin record

## Correlation Identifiers

Link evidence across system boundaries with the minimum needed:

- Request ID, Correlation ID, Trace ID
- Order ID, Transaction ID, Customer ID, Message ID
- Timestamp
