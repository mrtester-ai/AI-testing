# Senior QA Skills — Routing Index

A library of six QA skill playbooks plus five shared references. Each `SKILL.md` is a lean decision core; heavy templates, catalogues, and worked examples live in that skill's `references/` folder and are read only when needed.

## Which skill do I use?

| I need to… | Use |
|---|---|
| Plan testing — strategy, scope, estimates, entry/exit criteria, release gates, release readiness | **test-strategy-and-planning** |
| Design tests — scenarios, cases, coverage, traceability, regression suite | **test-case-design-and-management** |
| Automate — framework, tests, flaky tests, CI/CD, coverage/ROI | **test-automation-and-frameworks** |
| Execute/validate — web UI, REST API, integrations, auth, async, E2E | **web-api-and-integration-testing** |
| Handle a defect — report, triage, investigate, RCA, validate a fix | **defect-management-and-root-cause-analysis** |
| Lead — review artifacts, mentor, communicate risk, report, escalate | **quality-leadership-and-communication** |

**Rule of thumb:** strategy = *which* tests and *how much*; case-design = *which scenarios and techniques*; automation = *how to run them reliably*; web-api = *execute at the interface*; defect = *what failed and why*; leadership = *decide, communicate, improve*.

## Skills

| Skill | Tags |
|---|---|
| `test-strategy-and-planning/` | strategy · planning · risk-based-testing · release-readiness |
| `test-case-design-and-management/` | test-design · coverage · traceability |
| `test-automation-and-frameworks/` | automation · frameworks · ci-cd · flaky-tests |
| `web-api-and-integration-testing/` | api-testing · integration · ui-testing · e2e · auth |
| `defect-management-and-root-cause-analysis/` | defect-management · rca · triage · fix-validation |
| `quality-leadership-and-communication/` | leadership · communication · reporting · mentoring |

## Shared References

| Reference | Contents | Owner | Linked from |
|---|---|---|---|
| `shared/release-readiness.md` | READY / READY WITH KNOWN RISKS / CONDITIONAL / NOT READY; release templates | strategy | leadership, defect |
| `shared/severity-and-priority.md` | S1–S4, P0–P3, impact model | defect | case-design, strategy, web-api, leadership |
| `shared/evidence-templates.md` | evidence types, sanitization, request/response template | defect | web-api, case-design, strategy |
| `shared/ecommerce-coverage.md` | eCommerce coverage checklist and cross-system chain | strategy | case-design, web-api, defect, leadership |
| `shared/test-design-techniques.md` | technique catalogue, selection table, worked examples | case-design | leadership, web-api, strategy |

## Editing Rules

- Keep **decision logic and routing** in `SKILL.md`; move templates/checklists/catalogues to `references/`.
- Do not restate a shared reference — link it.
- Every skill states **When NOT to Use → use X** to prevent overlap.
- Keep frontmatter `name` and `description` intact (they drive triggering); extend via `metadata`.

## Notes

- Originals are preserved under `_original/` (pre-restructure backup).
- The per-skill `.zip` archives are now stale — regenerate them from the updated folders if you distribute them.
