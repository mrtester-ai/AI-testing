# Planning Templates (Reference)

**Owner:** `test-strategy-and-planning`.

## Ambiguities and Assumptions

| ID | Area | Question / Assumption | Testing Impact | Risk if Unresolved |
|---|---|---|---|---|

Do not block the whole strategy when reasonable assumptions can be made — label them and state their impact on coverage or estimates.

## Risk Register

| Risk ID | Area | Failure Scenario | Probability | Impact | Risk Level | Mitigation / Test Approach |
|---|---|---|---|---|---|---|

Risk level High/Medium/Low — see `shared/severity-and-priority.md`. Do not assign High just because a feature is large; weigh likelihood and impact.

## Test Approach

| Test Type | Scope | Priority | Rationale | Execution Approach |
|---|---|---|---|---|

## Estimates

| Activity | Scope | Estimated Effort | Dependencies | Assumptions |
|---|---|---:|---|---|

Include: requirement analysis · strategy · design · data prep · env setup · functional/API/integration/regression execution · exploratory · cross-browser/device · defect investigation · retest · automation · reporting · release verification. Prefer ranges when uncertain. State what could increase the estimate. Do not fabricate precision.

## Roles and Ownership

Requirement clarification · test preparation · execution · automation · environment support · defect fixing · business validation · release decision. Use role names when individuals are unknown.

## Quality Gates

| Gate | Criteria | Evidence | Status |
|---|---|---|---|
| Build readiness | Deploys successfully; environment usable | Deployment/env evidence | Not Assessed |
| Critical functionality | All P0 tests pass | Execution result | Not Assessed |
| Regression | Required suite completed | Regression report | Not Assessed |
| Defects | No unresolved release blockers | Defect report | Not Assessed |
| Integrations | Critical flows pass | API/integration evidence | Not Assessed |
| Release risk | Residual risks documented and accepted | QA summary | Not Assessed |

Never mark a gate passed without evidence.

## Coverage Matrix

| Requirement / Area | Risk | Test Type | Priority | Coverage | Status |
|---|---|---|---|---|---|

## Residual Risks

For each: description · impact · why it remains · mitigation · recommended owner · required acceptance.
