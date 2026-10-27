# Test Levels and Types (Reference)

**Owner:** `test-strategy-and-planning`. Select only those the change's risk requires.

## Test Levels

- **Unit** — isolated logic/functions.
- **Component** — one component below full UI/E2E.
- **API** — service contract and business rules.
- **Integration** — service boundaries and dependencies.
- **System** — integrated system behavior.
- **End-to-end** — critical business journeys across components.
- **User acceptance** — business/user validation.
- **Production verification** — post-deploy smoke/monitoring.

Prefer the lowest reliable level; keep enough E2E for critical journeys.

## Functional Testing

Business rules · validation · calculations · user interactions · state transitions · error handling.

## API Testing

Request/response structure · status codes · authentication · authorization · required/invalid fields · boundaries · error responses · persistence · idempotency where relevant.

## Integration Testing

Data mapping · successful communication · missing data · invalid responses · timeouts · retries · partial failures · asynchronous processing · duplicate requests/messages · downstream availability.

## End-to-End Testing

Typical eCommerce path: `Product → Cart → Checkout → Payment → Order → Fulfilment`. Use selectively — E2E is typically more expensive and fragile than lower-level tests.

## Regression Testing

Define focused regression from: direct change impact · shared components · dependencies · historical defects · critical journeys · high-risk integrations. Classify as: critical smoke · change-focused · integration · full.

## Exploratory Testing

Use for new functionality, complex interactions, poorly specified behavior, high-risk areas, areas with historical defects, and unexpected integration behavior.

## Compatibility Testing

Supported browsers · mobile · tablet · desktop · OS · responsive breakpoints. Only include combinations with meaningful product risk.

## Accessibility Testing

Keyboard navigation · focus handling · screen-reader compatibility · semantic structure · labels · error identification · color contrast · zoom/text scaling. Align with the agreed standard (e.g. WCAG) when defined.

## Performance Testing

Consider when the change may affect response time, page load, API latency, throughput, concurrency, resource use, DB queries, caching, search, checkout, or third-party calls. Types: baseline · load · stress · spike · endurance. Do not recommend performance testing merely because a release is large — link it to credible risk.

## Security Testing

Consider when the change affects authentication, authorization, customer data, payment, APIs, headers, sessions, cookies, file handling, input validation, admin functionality, third-party integrations, or platform dependencies. Consider relevant OWASP risks.
