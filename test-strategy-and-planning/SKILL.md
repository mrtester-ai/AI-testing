---
name: test-strategy-and-planning
description: >
  Creates risk-based test strategies, test plans, regression approaches,
  estimates, quality gates, and release-readiness recommendations. Use this
  skill when planning testing for a new feature, release, integration,
  platform change, migration, security update, incident fix, hotfix, or
  regression cycle; assessing QA scope and effort; determining required
  test types; defining entry and exit criteria; identifying quality risks;
  or preparing an evidence-based release recommendation.
metadata:
  version: 2.0.0
  owner: QA Practice
  tags: [test-strategy, planning, risk-based-testing, release-readiness]
---

# Test Strategy and Planning

## Purpose

Create practical, risk-based strategies and plans that give meaningful product-quality coverage and support evidence-based release decisions.

The objective is not to test everything equally. Identify where failure would matter most, define sufficient coverage for those risks, and communicate what is tested, what is not, and what residual risk remains.

## When to Use

Use when asked to: create a test strategy or plan · plan QA for a feature/release · assess the testing impact of a change · plan regression / smoke · estimate QA effort · determine required test types · plan testing for an integration, API, platform, dependency, security, incident-fix, hotfix, or regression cycle · define entry/exit criteria and release gates · assess release readiness · identify quality risks and dependencies · determine minimum acceptable coverage when time is limited · build a requirement-to-test coverage strategy · identify environment, data, tooling, or staffing needs.

## When NOT to Use

| Situation | Use instead |
|---|---|
| Designing the detailed test cases themselves | `test-case-design-and-management` |
| Building or maintaining automation | `test-automation-and-frameworks` |
| Investigating a specific defect or root cause | `defect-management-and-root-cause-analysis` |
| Manually validating UI/API/integration behavior | `web-api-and-integration-testing` |
| Leading QA, reviewing artifacts, reporting, mentoring | `quality-leadership-and-communication` |

## Core Responsibilities

- Analyze requirements, acceptance criteria, specs, architecture, designs, and known defects.
- Understand the customer journey and business impact of the change.
- Identify quality risks, assumptions, dependencies, constraints, and unknowns.
- Determine impacted systems, components, integrations, and regression areas.
- Define in/out of scope, select test levels and types, and prioritize by risk.
- Define environments, test data, tooling, ownership, and dependencies.
- Estimate QA effort with transparent assumptions.
- Define entry/exit criteria and evidence-based quality gates.
- Communicate untested areas and residual risk; give a clear release recommendation.

## Operating Principles

1. Do not plan all test types mechanically — select testing by the risk the change introduces.
2. Separate confirmed requirements from assumptions; never invent missing ones.
3. Document important unknowns explicitly.
4. Prioritize customer and business impact over test-case count.
5. Increase depth when probability or impact of failure is high; reduce it when risk is low and existing controls suffice.
6. Reuse existing regression coverage; avoid duplicating equivalent tests across levels.
7. Prefer the lowest effective test level that gives reliable evidence.
8. Include exploratory testing where uncertainty remains.
9. Treat release readiness as a risk decision, not a pass-rate calculation.
10. Never hide untested areas or unresolved high-impact risks.
11. Adapt the strategy as scope, implementation, defects, environments, or timelines change.

## Workflow

1. **Understand the change** — objective, journeys, changed components, architecture, APIs, data flows, config, infra, dependencies, platforms, existing tests, related defects. Classify the change type (see table).
2. **Identify ambiguities, assumptions, and unknowns** — record each with its testing impact and risk if unresolved.
3. **Change-impact analysis** — direct, upstream, downstream, shared components, data impact, regression impact.
4. **Identify and prioritize quality risks** — probability × impact across customer, revenue, transaction, financial, data-integrity, security, privacy, availability, performance, accessibility, compliance, compatibility, integration, operational, recoverability, regression.
5. **Define test objectives** (outcomes, not activities) and **scope** (in/out — every exclusion with reason and risk).
6. **Select test levels and types** — see `references/test-types.md`.
7. **Define minimum viable coverage** and **prioritize** coverage P0–P3.
8. **Plan environments and test data** — record differences from production that affect confidence.
9. **Estimate effort** with a transparent table and ranges where uncertain.
10. **Define ownership, entry criteria, exit criteria, and quality gates**.
11. **Monitor and adapt** during execution.
12. **Assess release readiness** — see `shared/release-readiness.md`.

## Decision Table — Change Type → Default Depth and Regression

| Change type | Default test levels | Regression scope | Must cover |
|---|---|---|---|
| **New functionality** | API + integration + targeted E2E | Focused around new + adjacent | All new rules, negative, boundaries |
| **Enhancement** | Same as the touched area | Focused on affected journeys | Changed behavior + old behavior preserved |
| **Bug fix** | Lowest level reproducing the bug | Direct + adjacent | Original repro + variants + side effects |
| **Hotfix / incident** | Minimal + production smoke | Critical journeys only | Original problem, fix, immediate area, shared components |
| **Integration / API change** | API + integration | Upstream/downstream consumers | Mapping, timeout, retry, duplicate, partial failure |
| **UI-only change** | Component/UI + focused manual | Focused (avoid full by default) | Reuse, responsive, browser, a11y, journey impact |
| **Security patch / platform upgrade** | Smoke + security + critical regression | Broad on shared layers | Auth, authz, sessions, headers, checkout, jobs, search |
| **Migration / DB change** | Integration + data reconciliation | Data-critical journeys | Mapping, persistence, rollback, reconciliation |
| **Config / feature-flag change** | Smoke across flag states | Flag-dependent surfaces | Both states, cache, environment differences |

This table is a **default**, not a rule — override it with risk.

## Coverage Priorities

| Priority | Meaning |
|---|---|
| **P0 Critical** | Must execute before release (auth for required journeys, checkout, payment, order creation, critical financial calc, security, data integrity). |
| **P1 High** | Execute before release unless explicitly accepted as residual risk. |
| **P2 Medium** | Execute when schedule permits after P0/P1. |
| **P3 Low** | Extended regression, exploratory follow-up, or post-release validation. |

Never prioritize by test-case order.

## Minimum Viable Coverage (constrained timeline)

P0 journeys · changed functionality · highest-risk integrations · critical negative scenarios · critical data integrity · critical security controls · focused regression around changed components · production smoke where appropriate. Explicitly state what is deferred and the risk created.

## Entry / Exit Criteria (defaults)

**Entry:** requirements understood and testable · build deployed · critical integrations available · env stable · data available · blocking env defects resolved · flags configured.

**Exit:** 100% of P0 executed and passed · required P1 done · no release-blocking defects · no critical data-integrity/security issues · required integration and regression journeys passed · known defects dispositioned · untested areas documented · residual risk accepted by the decision-maker.

Do not use overall pass percentage alone (95% passed is insufficient if checkout failed).

## Default Output Structure

1. Executive Summary · 2. Scope (in/out) · 3. Assumptions and Dependencies · 4. Risk Assessment · 5. Test Approach · 6. Regression Strategy · 7. Environment and Test Data · 8. Test Estimates · 9. Execution Plan · 10. Entry Criteria · 11. Exit Criteria · 12. Quality Gates · 13. Coverage Matrix · 14. Residual Risks · 15. Release Recommendation.

## References

- `shared/release-readiness.md` — canonical release categories, recommendation and summary templates
- `shared/severity-and-priority.md` — severity/priority and impact model
- `shared/ecommerce-coverage.md` — eCommerce coverage checklist
- `references/test-types.md` — full test-type and level catalogue
- `references/special-scenarios.md` — hotfix, security patch, integration, UI-only, critical eCommerce
- `references/templates.md` — risk register, estimates, coverage matrix, quality gates
- `references/example-strategy.md` — a fully worked strategy example
