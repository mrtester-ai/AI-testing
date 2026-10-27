# Integration Testing (Reference)

**Owner:** `web-api-and-integration-testing`.

## Data Mapping

Verify source fields transform correctly into destination fields.

| Source Field | Source Value | Destination Field | Expected Value | Actual |
|---|---|---|---|---|

Watch: dates · time zones · currency · decimal precision · boolean conversion · enum mapping · null handling · identifiers.

## Data Ownership

Identify the authoritative system for important values: customer · price · inventory · order · shipment · refund. Do not assume the displayed value is the authoritative value.

## Synchronous Integration

Verify: request sent · response received · timeout · validation · mapping · error handling · customer-visible result.

## Asynchronous Integration

For queues, events, webhooks, scheduled jobs verify: event created · correct payload · correct destination · processing occurs · final state becomes consistent · duplicate handling · retry behavior · poison/dead-letter handling where available · delayed processing · out-of-order events.

Account for expected eventual consistency. Do not classify an initial temporary state as a defect if the contract explicitly permits asynchronous completion.

## Retry Testing

Where retry is supported validate: number of attempts · delay/backoff · retryable vs non-retryable failure · final failure state · user-visible state · duplicate prevention · observability. A technical retry must not create duplicate business transactions.

## Timeout Testing

Validate: client timeout · service timeout · external dependency timeout · user-visible behavior · transaction status · retry behavior · recovery behavior.

> **Key question:** did the remote system process the transaction even though the caller timed out? Critical for payment and order operations.

## Partial Failure Testing

For multi-system workflows, consider failures after some steps succeed (e.g. payment authorized → order creation fails). Determine the expected: retry · rollback · cancellation · compensation · manual recovery · pending state. Do not assume rollback unless defined.

## Reconciliation Testing

Compare records between source and destination: record exists · identifier matches · status matches · quantity · price · tax · currency · timestamp reasonable · expected fields mapped. Report discrepancies precisely.

## Observability

Good integration testing depends on traceability. Useful fields: correlation ID · request ID · trace ID · transaction ID · order ID · message ID · timestamp. When recurring failures are hard to investigate, recommend structured logging, correlation IDs, distributed tracing, monitoring, alerts, and integration dashboards.
