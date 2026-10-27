# Quality Metrics (Reference)

**Owner:** `quality-leadership-and-communication`. Metrics should help teams make decisions or improve — not merely populate dashboards.

## Coverage

Critical requirement coverage · critical user-journey coverage · risk coverage · regression coverage · automation coverage where meaningful.

## Execution

Planned vs executed · pass/fail/block status · P0/P1 execution status · blocked test duration.

## Defects

Defects by severity · by affected area · defect ageing · reopened defects · production escapes · recurring defects.

## Delivery Quality

Escaped-defect trend · regression-defect trend · change-failure patterns · production incidents.

## Automation

Automated regression coverage · execution duration · failure reliability · **flaky-test rate** · feedback time · maintenance effort.

## Process

Requirement defects found before development · test-environment downtime · repeated blockers · test-data delays · defect recurrence.

## Interpretation Rules

Never interpret a metric in isolation:

- **98% pass rate** can still be unacceptable if the failed 2% includes payment or order placement.
- **100 open defects** may matter less than five unresolved critical checkout defects.
- **90% automation coverage** proves little if assertions are weak or tests are unreliable.

Use metrics to answer questions, not to fill a dashboard.
