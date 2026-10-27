# Release Readiness (Shared Reference)

Canonical release-readiness definitions and templates.

**Owned by:** `test-strategy-and-planning`.
**Linked from:** `quality-leadership-and-communication`, `defect-management-and-root-cause-analysis`.

Do not redefine these categories in other skills — link here instead.

## Recommendation Categories

| Category | Meaning | Typical Trigger |
|---|---|---|
| **READY** | Required quality gates are satisfied and no material unresolved risk prevents release. | All P0/P1 pass, no blockers, integrations verified. |
| **READY WITH KNOWN RISKS** | Required critical coverage passes, but known non-blocking residual risks remain and should be explicitly accepted. | P0/P1 pass; a documented low/medium risk is accepted by the release owner. |
| **CONDITIONAL / HOLD** | Evidence is incomplete or important testing is blocked. Release waits until stated conditions are met. | Blocked environment, missing integration, incomplete regression. |
| **NOT READY** | One or more unacceptable risks, critical failures, or release-blocking defects remain. | Failed checkout/payment, critical security or data-integrity issue. |

## Jurisdiction

- QA provides the **evidence-based recommendation**.
- The authorized **release owner** makes the final decision per organizational policy.
- Never recommend READY based on an overall pass percentage alone. A 95% pass rate is insufficient if the failed 5% includes checkout or payment.

## Evaluation Checklist

Before recommending, evaluate:

- Planned vs. actual executed coverage
- P0 / P1 status
- Open, deferred, and blocked defects
- Untested areas
- Environment limitations and production differences
- Integration results
- Security, performance, and data-integrity concerns
- Residual risk and its acceptance

## Release Recommendation Template

### QA Recommendation
**Status:** READY / READY WITH KNOWN RISKS / CONDITIONAL / NOT READY

- **Change:** Brief description.
- **Coverage completed:** Functional / Integration / Regression / E2E / Compatibility / Security / Performance — only what was actually performed.
- **Critical results:** Status of critical business journeys.
- **Open defects:** Material defects and business impact.
- **Untested / blocked areas:** Important gaps.
- **Residual risks:** Remaining exposure.
- **Mitigation:** Workaround, monitoring, rollback, or follow-up testing.
- **Rationale:** Why QA recommends this outcome.
- **Decision owner:** Role responsible for the final call.

## Release Summary Template

**Recommendation:** READY / READY WITH KNOWN RISKS / CONDITIONAL / NOT READY

- **Coverage:** Planned / Executed / Passed / Failed / Blocked / Not executed
- **Critical coverage:** P0 / P1 / Critical E2E / Integration / Regression
- **Defects:** Critical / High / Medium / Low
- **Untested / blocked areas:** Areas without sufficient evidence
- **Residual risks:** Risks remaining after completed testing
- **Rationale:** Short, evidence-based explanation
