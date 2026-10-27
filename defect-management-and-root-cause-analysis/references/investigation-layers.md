# Investigation Layers (Reference)

**Owner:** `defect-management-and-root-cause-analysis`. Narrow the failure progressively — do not assume the layer where the symptom appears is the layer causing it.

## UI Layer

Rendered state · validation · browser console · JavaScript errors · network requests · responsive behavior · session state.

## API Layer

Endpoint · HTTP method · request · response · status code · authentication · authorization · headers · validation · payload mapping · timing.

## Application Layer

Business logic · configuration · feature flags · cache · session · background jobs · indexing.

## Data Layer (authorized)

Persistence · data mapping · record state · calculations · duplicate records · transaction state.

## Integration Layer

Request sent · response received · authentication · mapping · timeout · retry · queue processing · duplicate handling · partial failure · asynchronous delay.

## Infrastructure Layer

CDN · cache · WAF · load balancer · proxy · network · environment configuration.

## Comparison Matrix

| Condition | Working Case | Failing Case | Observation |
|---|---|---|---|
| Environment | Production | Staging | Failure only on staging |
| User | Logged in | Guest | Both affected |
| Browser | Chrome | Safari | Both affected |

Comparison dimensions: staging vs production · old vs new build · guest vs logged-in · customer group A vs B · browser A vs B · mobile vs desktop · product type A vs B · endpoint A vs B · valid vs invalid data · cache on/off · flag on/off · integration available/unavailable · before vs after change. Change one meaningful condition at a time. Do not claim correlation as causation.

Evidence types and sanitization: `shared/evidence-templates.md`.
