---
name: defect-management-and-root-cause-analysis
description: >
  Investigates, documents, triages, analyzes, and validates software defects
  using evidence-driven QA practices. Use this skill when reporting bugs,
  investigating unexpected behavior, triaging incidents, comparing expected
  versus actual behavior, analyzing regressions, performing root-cause analysis,
  validating fixes, planning defect-focused regression, writing Jira defect
  reports or validation comments, or identifying recurring quality problems.
metadata:
  version: 2.0.0
  owner: QA Practice
  tags: [defect-management, rca, triage, fix-validation]
---

# Defect Management and Root Cause Analysis

## Purpose

Manage defects from discovery through investigation, triage, fix validation, regression, and closure, using objective evidence to establish what failed, under which conditions, what impact it has, what likely caused it, whether the fix is complete, and what should reduce recurrence.

The objective is not merely to report that something is broken — it is to give engineering and product enough reliable information to understand, reproduce, prioritize, resolve, and safely close the issue.

## When to Use

Use when asked to: report a defect · create/improve a Jira bug · rewrite a defect report or Jira comment · investigate unexpected behavior · compare expected vs actual · decide whether something is a defect · improve reproduction steps · assess severity/priority · investigate an intermittent failure or regression · analyze possible root causes · perform RCA · review logs/API/UI/config for an issue · determine whether a fix is complete · validate a fix · define post-fix regression · assess reopening · summarize QA validation evidence · analyze repeated/escaped defects · recommend preventive actions.

## When NOT to Use

| Situation | Use instead |
|---|---|
| Designing tests (before a failure exists) | `test-case-design-and-management` |
| Planning scope, strategy, or release gates | `test-strategy-and-planning` |
| Executing/inspecting live UI/API/integration behavior | `web-api-and-integration-testing` |
| Leading QA, triage facilitation, reporting, mentoring | `quality-leadership-and-communication` |

## Operating Principles

1. Unexpected behavior is not automatically a product defect.
2. Establish expected behavior before concluding actual behavior is wrong.
3. Distinguish facts, observations, hypotheses, and confirmed causes.
4. Never present a suspected cause as the root cause without evidence.
5. A failing component is not necessarily the root cause.
6. A disappearing symptom does not prove the underlying defect is fixed.
7. Severity and priority are different — never interchangeable.
8. Capture enough evidence for someone else to reproduce or investigate.
9. Never include credentials, tokens, or PII in defect evidence.
10. Prefer minimal deterministic reproduction over long workflows.
11. Test the original failure first when validating a fix.
12. Regression depth reflects the technical and business impact.
13. State environment limitations and incomplete validation.
14. Keep communication factual, professional, concise, and collaborative.
15. Do not blame individuals during RCA.

## Workflow

1. **Establish the observation** — record exactly what was observed (feature, journey, user type, data, environment, build, browser, config, time, action, actual result). Do not diagnose yet.
2. **Establish expected behavior** — from requirements, stories, acceptance criteria, business rules, specs, contracts, designs, or agreed behavior. If unclear: "Expected behavior requires confirmation." Never invent it.
3. **Reproduce** — capture environment, build, preconditions, account, permissions, data, config, steps, result, timestamp, frequency (Always / Intermittent / specific data/account/browser/env / Not reproduced). Quantify intermittent behavior only when enough runs support it.
4. **Minimize the reproduction** — smallest reliable sequence; remove steps that do not affect the outcome.
5. **Compare working vs failing conditions** — change one meaningful condition at a time. Correlation is not causation.
6. **Collect evidence** — relevant UI, API, server, data, and environment evidence only; sanitize. See `shared/evidence-templates.md`.
7. **Investigate across layers** — see `references/investigation-layers.md`.
8. **Perform RCA** when justified — see the model below and `references/rca-techniques.md`.
9. **Validate the fix** — see workflow below.
10. **Decide close / reopen / follow-up** — see criteria below and `references/report-and-communication.md`.

## The RCA Model (core)

Perform formal RCA when justified by impact, recurrence, complexity, or request (production incident, repeated regression, escaped/critical defect, data-integrity or security issue, complex integration failure).

Separate these clearly — the distinction is the whole point:

| Element | Meaning |
|---|---|
| **Symptom** | What the user or system observed. |
| **Trigger** | The conditions required for the failure. |
| **Contributing factor** | Increased likelihood/impact but not sufficient alone. |
| **Hypothesis** | A possible explanation, not yet confirmed. |
| **Root cause** | The underlying **confirmed** cause. |
| **Escape cause** | Why existing controls failed to catch it before the affected environment. |
| **Corrective action** | Fixes the immediate defect. |
| **Preventive action** | Reduces recurrence. |

**Confidence:** Confirmed (direct evidence) · Likely (strong evidence, not fully confirmed) · Possible (plausible, needs investigation) · Unknown (insufficient evidence). Never present Likely/Possible as confirmed.

> **Example:** Symptom — confirmation shows the wrong pickup store. Trigger — customer changes the store during checkout. Root cause — confirmation reads stale cart store data instead of the final order fulfilment data. Escape cause — regression validates store selection but not the persisted order store. Corrective — populate from the final order. Preventive — add an E2E assertion comparing selection, order, and confirmation.

## Severity and Priority

See `shared/severity-and-priority.md` for the canonical S1–S4 and P0–P3 scales and the impact model. Do not restate them here.

## Fix Validation Workflow

1. **Confirm the correct build** — environment, deployment, fix version, config, flags.
2. **Re-run the original reproduction** — original path, equivalent data/conditions.
3. **Verify the business outcome** — do not stop when an error message disappears (product actually added, order actually created, correct total persisted).
4. **Test important variations** — positive, negative, boundary, alternate user/data, repeated action (only what is relevant).
5. **Targeted regression** — direct, adjacent, integration, historical, critical-journey.
6. **Check side effects** — new errors, data inconsistency, duplicates, UI/integration regression.
7. **Capture evidence.**
8. **Set status** — PASS / FAIL / PARTIALLY PASS / BLOCKED / NEEDS CLARIFICATION. Never PASS if important acceptance conditions remain unverified.

## Reopen and Closure Criteria

**Reopen when:** original still reproducible · fix addresses only some conditions · expected business behavior still wrong · high-impact regression introduced · data still incorrect · works only in a limited configuration without justification · acceptance criteria not fully met. Do not reopen for an unrelated new issue — raise a separate defect.

**Ready to close when:** correct build tested · original no longer reproducible · expected behavior verified · negative/boundary scenarios pass · targeted regression passes · no unacceptable side effect · evidence captured · limitations documented · residual risk accepted.

## Default Output Structure

1. Defect Summary · 2. Expected vs Actual · 3. Reproduction Conditions · 4. Impact Assessment · 5. Evidence · 6. Investigation Findings (confirmed / hypotheses / unknowns) · 7. Root Cause (symptom, trigger, cause, confidence, escape cause) · 8. Fix Validation · 9. Residual Risk · 10. Recommendation (close / reopen / investigate / separate defect / clarify requirement / more regression).

## References

- `shared/severity-and-priority.md` — severity, priority, and impact model
- `shared/evidence-templates.md` — evidence capture and sanitization
- `shared/ecommerce-coverage.md` — eCommerce coverage / cross-system chain
- `references/investigation-layers.md` — layer-by-layer investigation
- `references/rca-techniques.md` — Five Whys, change analysis, timeline, correlation, fishbone, fault-tree, regression analysis
- `references/report-and-communication.md` — defect report template, Jira standards, validation comments, pattern analysis, preventive actions
- `references/example-rca.md` — a fully worked RCA example
