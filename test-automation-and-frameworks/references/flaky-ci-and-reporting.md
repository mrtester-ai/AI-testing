# Flaky Tests, CI/CD, Reporting, and ROI (Reference)

**Owner:** `test-automation-and-frameworks`. These sections complete the automation skill.

## Flaky-Test Investigation

**A flaky test is a defect in the testing system.** A test is flaky if it produces different results across identical runs.

### Classify the failure first

| Class | Typical cause | Action |
|---|---|---|
| **Product defect** | Real race, intermittent backend bug | Fix the product; keep the test |
| **Automation defect** | Bad wait, brittle selector, ordering, shared state | Fix the test |
| **Environment flake** | Slow/unstable env, dependency, network | Stabilize env or isolate the test |
| **Test-data flake** | Shared/expired records, collisions | Make data deterministic and unique |

### Triage workflow

1. Reproduce with the failure's trace/report; do not rerun blindly.
2. Identify whether it fails in isolation, under parallel load, or on a specific env.
3. Look for: fixed sleeps, implicit ordering, shared mutable data, unawaited async, non-deterministic selectors, external dependencies, clock/timezone.
4. Fix the root cause. **Do not** mask it with retries.
5. If it cannot be fixed immediately, **quarantine** it (exclude from the gate) and track it as a defect — never leave it silently red.
6. Add a regression guard so the same flakiness class is caught earlier.

### Retries

Retries must never be used to hide instability. A single retry to absorb genuine infra noise is acceptable **only** when the underlying reliability is separately measured — and the flaky rate must be tracked.

## CI/CD Integration

Run the right layer at the right stage:

| Stage | Runs | Gate? |
|---|---|---|
| Pull request | Unit, component, fast API | Yes — must be fast & reliable |
| Merge to main | API + integration + contract | Yes |
| Deploy to env | UI smoke, critical E2E | Yes for release |
| Nightly | Full regression, cross-browser, performance | No (reports) |

Rules:
- Keep PR feedback within team tolerance; parallelize and shard.
- Never gate the merge on a flaky suite — quarantine flaky tests first.
- Cache dependencies; run independent suites concurrently.
- Fail fast on smoke before running the long suite.

**Pipeline skeleton (GitHub Actions):**

```yaml
jobs:
  pr:
    steps:
      - run: npm ci
      - run: npx playwright test tests/smoke tests/api --shard=${{ matrix.shard }}/4
    strategy:
      matrix: { shard: [1, 2, 3, 4] }
  nightly:
    if: github.event_name == 'schedule'
    steps:
      - run: npx playwright test tests/regression tests/e2e
```

## Reporting and Diagnostics

A failure must answer: **what failed · expected vs. actual · where**. Provide:
- A structured reporter (JUnit/JSON) consumable by CI.
- On failure: trace, screenshot, and video (Playwright: `trace: 'on-first-retry'`).
- The assertion message, not just a stack trace.
- Environment/build metadata and the exact data used.

## Coverage and ROI Assessment

Track and interpret in context (never in isolation):
- Automated regression coverage of critical journeys
- Execution duration and feedback time
- **Flaky-test rate** (should trend down)
- Failure reliability (signal vs. noise)
- Maintenance effort per suite
- Escaped defects that automation *could* have caught

ROI model:

```
Value = manual effort avoided
      + earlier defect detection
      + repeatability / consistency
      + release confidence
      − implementation cost
      − maintenance cost
      − infrastructure cost
      − failure-triage cost
```

Interpretation rules:
- High coverage with weak assertions ≠ quality.
- 100% green on a flaky suite ≠ confidence.
- A large slow suite that people disable has negative value.

Retire or refactor suites where maintenance cost exceeds the value delivered.
