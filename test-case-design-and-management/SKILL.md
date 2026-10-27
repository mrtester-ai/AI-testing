---
name: test-case-design-and-management
description: >
  Designs, reviews, organizes, and maintains risk-based test scenarios and
  execution-ready test cases. Use this skill when translating requirements,
  acceptance criteria, designs, business rules, or defects into tests; creating
  regression suites; reviewing existing test coverage; identifying coverage
  gaps; optimizing redundant tests; creating traceability; or preparing tests
  for execution, automation, and release sign-off.
metadata:
  version: 2.0.0
  owner: QA Practice
  tags: [test-design, coverage, traceability, risk-based-testing]
---

# Test Case Design and Management

## Purpose

Design, organize, review, and maintain clear, efficient, traceable tests that uncover defects and provide reliable evidence that expected business behavior works.

The objective is **not** the largest possible number of test cases. It is the strongest risk coverage with the smallest practical, maintainable, reusable test set.

## When to Use

Use when asked to: translate requirements/acceptance criteria into scenarios · create functional, integration, system, E2E, regression, smoke, or exploratory tests · review tests for gaps, duplication, or ambiguity · optimize a regression suite · create a coverage or traceability matrix · identify positive/negative/boundary/error scenarios · prioritize tests for a release or hotfix · identify automation candidates · prepare execution-ready cases for Jira, Azure DevOps, TestRail, Zephyr, Xray, Excel, etc.

## When NOT to Use

| Situation | Use instead |
|---|---|
| Planning scope, strategy, estimates, entry/exit criteria, release gates | `test-strategy-and-planning` |
| Building or maintaining an automated suite, fixing flaky tests | `test-automation-and-frameworks` |
| Investigating a specific failure, root cause, or fix validation | `defect-management-and-root-cause-analysis` |
| Exercising live UI / API / integration behavior end to end | `web-api-and-integration-testing` |
| Leading QA, reviewing artifacts, mentoring, reporting | `quality-leadership-and-communication` |

## Core Responsibilities

- Derive test conditions from requirements, acceptance criteria, designs, business rules, specs, and known risks.
- Identify unclear, missing, conflicting, or untestable requirements.
- Cover positive, negative, boundary, alternate, permission, state-transition, integration, and error-handling paths.
- Select test-design techniques based on the problem.
- Prioritize by business impact, probability of failure, change impact, and detectability.
- Produce reproducible steps with explicit, observable expected results.
- Maintain traceability between requirements, risks, test cases, defects, and evidence.
- Remove redundant tests without weakening meaningful coverage.
- State assumptions, exclusions, dependencies, and coverage limitations.
- Recommend exploratory testing for uncertain or high-risk areas.

## Operating Principles

1. Do not invent missing requirements or expected behavior.
2. Separate confirmed requirements from assumptions and recommendations.
3. Ask focused clarification questions when missing information affects expected results; otherwise proceed on documented assumptions.
4. Prioritize business outcomes over implementation details.
5. Use deeper coverage for high-risk behavior, lighter coverage for low risk.
6. Never create multiple tests verifying the same condition without added risk coverage.
7. Make every expected result objective, observable, and independently verifiable.
8. Keep test data controlled, safe, and environment-appropriate.
9. Consider upstream and downstream impact for integrations.
10. Never claim complete coverage when requirements, environments, integrations, or data are incomplete.

## Workflow

1. **Review source material** — requirements, stories, acceptance criteria, specs, designs, API contracts, business rules, defects, existing tests, incidents.
2. **Extract atomic testable conditions** — for each: actor, trigger, preconditions, input, rule, state, expected output, persistence, dependencies, failure behavior.
3. **Identify ambiguities and gaps** — missing expected results, conflicting rules, undefined limits/permissions/error handling, unclear transitions/integration/retry behavior.
4. **Identify risks** — quantify business, customer, financial, security, complexity, frequency, change, integration, historical, recoverability, and detectability. Classify **High / Medium / Low** (see `shared/severity-and-priority.md`).
5. **Select test-design techniques** — see `shared/test-design-techniques.md` (selection table + worked technique examples).
6. **Build coverage** — see `references/coverage-dimensions.md`. Apply only the dimensions relevant to the feature. eCommerce specifics: `shared/ecommerce-coverage.md`.
7. **Prioritize** — see table below.
8. **Write execution-ready cases** — see `references/test-case-templates.md`.
9. **Review and optimize** the suite (dedupe, strengthen, remove false confidence).
10. **Maintain traceability** — map requirements/risks → test IDs (table below).
11. **Identify automation candidates** — and the lowest reliable level (unit / component / API / integration / UI / E2E).

## Priority Model

| Priority | Meaning |
|---|---|
| **P0 Critical** | Must pass before release. Revenue, security, order placement, payment, critical data integrity, complete business blockage. |
| **P1 High** | Important business behavior, heavily used functionality, major integration, high change impact. |
| **P2 Medium** | Standard behavior, moderate impact, or a practical workaround. |
| **P3 Low** | Low-risk, uncommon, cosmetic, non-blocking. |

Explain why a scenario receives P0 or P1. When time is limited, provide a recommended execution order.

## Traceability Matrix Format

| Requirement ID | Summary | Risk | Test Case IDs | Coverage Status | Gap / Comment |
|---|---|---|---|---|---|

Coverage status: Covered · Partially Covered · Not Covered · Blocked · Not Testable · Clarification Required.

Do not mark covered when only the happy path is tested and material negative/boundary risks remain.

## When NOT to Automate

Avoid immediate automation when tests are highly volatile, exploratory, primarily visual/subjective, dependent on unstable third-party systems, rarely executed, hard to make deterministic, or more expensive to maintain than to run manually. Otherwise prefer the lowest reliable level.

## Default Output Structure

1. Requirement Summary · 2. Assumptions and Clarification Questions · 3. Risk Assessment · 4. Test Conditions and Coverage Map · 5. Test-Design Techniques Used · 6. Detailed Test Cases · 7. Exploratory Charters · 8. Traceability Matrix · 9. Coverage Gaps and Limitations · 10. Regression and Automation Recommendations · 11. Release-Critical Checklist.

## Before Finalizing

- [ ] Requirements and atomic conditions identified; ambiguities documented.
- [ ] Positive, negative, boundary, permission, state, and integration scenarios considered.
- [ ] High-risk requirements have sufficient depth; low-risk not over-tested.
- [ ] Expected results are explicit and observable; data, evidence, and cleanup documented.
- [ ] Tests are independent where practical; duplicate/low-value tests removed.
- [ ] Requirements, risks, and tests are traceable; gaps and remaining risk stated.

## References

- `shared/test-design-techniques.md` — technique catalogue, selection table, worked examples
- `shared/severity-and-priority.md` — severity/priority and impact model
- `shared/ecommerce-coverage.md` — eCommerce coverage checklist
- `shared/evidence-templates.md` — evidence capture and sanitization
- `references/coverage-dimensions.md` — full coverage dimension catalogue
- `references/test-case-templates.md` — minimal and full test-case templates
- `references/example-test-suite.md` — a fully worked example
