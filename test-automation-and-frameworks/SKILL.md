---
name: test-automation-and-frameworks
description: >
  Designs, implements, reviews, and improves maintainable test automation
  frameworks and automated quality checks across UI, API, component,
  integration, contract, and end-to-end testing. Use this skill when selecting
  automation candidates, designing automation architecture, writing or reviewing
  automated tests, improving flaky tests, creating reusable fixtures and test
  data, integrating automated checks into CI/CD, optimizing execution time,
  or assessing automation coverage and return on investment.
metadata:
  version: 2.0.0
  owner: QA Practice
  tags: [automation, frameworks, ci-cd, flaky-tests, playwright]
---

# Test Automation and Frameworks

## Purpose

Build and maintain reliable automated checks that give fast feedback, reduce repetitive manual effort, protect critical business behavior, and support safe continuous delivery.

Automation is not the objective. The objective is reliable, maintainable evidence about product quality at the **lowest appropriate test level** within an acceptable feedback time.

A good suite is: valuable · reliable · deterministic · maintainable · fast enough · easy to diagnose · safe to rerun · CI/CD-appropriate · aligned with risk.

## When to Use

Use when asked to: decide what to automate · create an automation strategy · design a framework · write or review automated tests · convert suitable manual tests · automate web/API/integration testing · create contract tests · select or compare tools · create Playwright/API tests · improve flaky tests · optimize execution · design fixtures or test data · integrate checks into CI/CD · define PR checks · review automation coverage · analyze automation failures · improve reporting · tell whether a failing test is a product defect · retire low-value tests.

## When NOT to Use

| Situation | Use instead |
|---|---|
| Deciding what to test, scope, strategy, estimates, gates | `test-strategy-and-planning` |
| Designing manual, exploratory, or scripted test cases | `test-case-design-and-management` |
| Confirming a specific failure is a product defect or RCA | `defect-management-and-root-cause-analysis` |
| Manually exercising live UI / API / integration behavior | `web-api-and-integration-testing` |

## Core Responsibilities

- Identify candidates by risk, value, repeatability, stability, execution cost, and maintenance cost.
- Select the appropriate test level and tools (based on stack and team capability).
- Design maintainable architecture; build deterministic setup/cleanup.
- Use stable selectors and reliable synchronization; write meaningful business assertions.
- Keep tests isolated; protect configuration and secrets.
- Integrate into CI/CD; optimize execution without losing risk coverage.
- Produce useful failure diagnostics; investigate flaky tests systematically.
- Distinguish product, automation, environment, and test-data failures.
- Monitor effectiveness; refactor or retire automation that no longer earns its place.

## Operating Principles

1. Do not automate a test just because it can be automated.
2. Prefer the lowest reliable test level that verifies the behavior.
3. Use UI automation selectively; keep E2E focused on critical journeys.
4. Prefer API/component/integration tests when they give equivalent confidence faster.
5. Automation must assert the business outcome — a passing test with no real assertion is worthless.
6. Avoid fixed sleeps when deterministic synchronization exists.
7. Tests must not depend on execution order; minimize shared mutable data.
8. A failed test must provide enough evidence to diagnose it.
9. **A flaky test is a defect in the testing system** — investigate it, never paper over it with retries.
10. Test code gets version control and code review like any other code.
11. Never hard-code secrets.
12. Test count and code coverage alone do not demonstrate quality.
13. Automation must evolve with product risk.

## Automation Selection

Before automating, assess value:

| Factor | Low | Medium | High |
|---|---|---|---|
| Business risk | Minor | Important | Critical |
| Execution frequency | Rare | Regular | Every build/release |
| Manual effort | Minimal | Moderate | Expensive |
| Product stability | Volatile | Evolving | Stable |
| Maintenance cost | High | Moderate | Low |
| Reuse | One scenario | Several | Broad |

**Prefer automating:** frequent, business-critical, stable, deterministic, data-driven, manual-expensive, multi-config/multi-browser, API-testable, smoke/regression scenarios.

**Be cautious with:** volatile, exploratory, visual/subjective, rarely run, unstable-dependency, hard-to-determinize, or cheaper-to-run-manually cases. Reassess later — do not permanently exclude.

ROI model (conceptual): `Value = manual effort avoided + earlier detection + repeatability + release confidence − implementation − maintenance − infrastructure − failure triage`. See `references/flaky-ci-and-reporting.md`.

## Test-Level Selection

| Level | Best for |
|---|---|
| **Unit** | Business logic, calculations, transformations, validators (usually engineering-owned) |
| **Component** | A component's behavior below full UI/E2E |
| **API** | Business rules, validation, auth/authz, CRUD, contracts, errors, boundaries |
| **Integration** | Service boundaries, mapping, persistence, queues, events, webhooks, retry |
| **Contract** | Provider/consumer compatibility across independently deployed services |
| **UI** | Behavior that genuinely needs a browser (navigation, JS, responsive, a11y interaction) |
| **E2E** | Critical business journeys only (Product → Cart → Checkout → Payment → Order) |

Default distribution: many fast low-level checks · moderate API/integration · few UI/E2E. Do not enforce a fixed pyramid ratio — optimize for fast, reliable confidence.

## Execution Model (essentials)

- Structure each test: **Arrange → Act → Assert** (+ Cleanup).
- Tests independently executable where practical; avoid chained create→modify→delete flows.
- Controlled test data: API-generated, fixtures/factories, unique identifiers (`test-user-{timestamp}@example.test`), clean up.
- Externalize config (base URLs, browsers, envs, flags, endpoints, accounts).
- Stable selectors, in order: accessible role/name → explicit test id → stable semantic attribute → stable CSS. Avoid deep DOM paths, generated classes, position, dynamic IDs, changeable text.
- Never hard-code secrets; use the CI/CD secret store and keep them out of logs, screenshots, traces, reports, and VCS.

Details and examples: `references/framework-and-execution.md`.

## Flaky and Failing Tests

- Classify first: **product defect · automation defect · environment flake · test-data flake**.
- A flaky test is a defect — quarantine it, find the root cause (race, wait, ordering, shared state, external dependency), fix it; do not retry-to-green.
- Retries must never hide instability.
- Workflow and triage checklist: `references/flaky-ci-and-reporting.md`.

## CI/CD Integration

- Run the right layer at the right stage: fast unit/component on PR; API/integration on merge; UI/E2E smoke on deploy; full regression nightly.
- Gate merge on fast, reliable checks — never make a flaky suite a hard gate.
- Keep total feedback time within team tolerance; parallelize and shard.
- Details and a pipeline skeleton: `references/flaky-ci-and-reporting.md`.

## Reporting and Diagnostics

A failure must answer: what failed, expected vs. actual, and where. Use structured reporters, attach trace/screenshot/video on failure, and surface the assertion message — not just a stack trace. See `references/flaky-ci-and-reporting.md`.

## Default Output Structure

1. Automation Recommendation · 2. Candidate Assessment (value table) · 3. Test-Level & Tool Choice · 4. Framework/Structure · 5. Data, Config & Secrets · 6. CI/CD Integration · 7. Flakiness & Diagnostics Plan · 8. Coverage & ROI · 9. Risks/Open Questions.

## Before Finalizing

- [ ] Each candidate justified by value, not convenience.
- [ ] Right test level chosen; E2E kept minimal.
- [ ] Assertions verify business outcomes.
- [ ] Tests are independent and deterministic; no fixed sleeps.
- [ ] Data is controlled and cleaned; secrets are externalized.
- [ ] CI integration and feedback time are defined.
- [ ] Flaky-test handling and diagnostics are addressed.

## References

- `shared/ecommerce-coverage.md` — eCommerce coverage checklist
- `references/framework-and-execution.md` — framework structure, config, data, selectors, code
- `references/flaky-ci-and-reporting.md` — flaky triage, CI/CD stages, ROI, reporting
- `references/example-framework.md` — a worked Playwright framework example
