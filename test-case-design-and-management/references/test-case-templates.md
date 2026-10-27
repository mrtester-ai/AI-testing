# Test-Case Templates (Reference)

**Owner:** `test-case-design-and-management`. Use the **minimal** template for simple cases; the **full** template for P0/P1 or high-risk cases.

## Minimal Template

| Field | Content |
|---|---|
| ID / Title | Unique ID + behavior under test |
| Requirement ID | Story / acceptance criterion / rule |
| Priority | P0 / P1 / P2 / P3 |
| Preconditions | Required state and data |
| Steps | Ordered, reproducible actions |
| Expected Result | Observable outcome (single, objective) |

## Full Template

| Field | Description |
|---|---|
| ID / Title | Unique identifier and concise behavior under test |
| Requirement ID | User story, acceptance criterion, Jira item, business rule, spec |
| Requirement / Risk | Requirement covered and risk addressed |
| Test Type | Functional, Integration, E2E, Regression, Smoke, Exploratory, Security, Performance, Compatibility |
| Priority | P0, P1, P2, P3 |
| Risk Level | High, Medium, Low |
| Preconditions | Required configuration, user, system, and data state |
| Test Data | Exact values, accounts, products, configuration, setup |
| Steps | Ordered and reproducible actions |
| Expected Results | Observable outcomes for important actions |
| Evidence | Screenshots, logs, API responses, DB records, emails |
| Automation Candidate | Yes / No / Conditional + short reason |
| Cleanup | State reset or data removal required |

## Writing Clear Steps and Expected Results

**Steps must:** start from a defined state · use clear actions · avoid hidden assumptions · include exact input values · be reproducible by another tester · avoid unnecessary navigation detail · avoid combining unrelated validations.

**Expected results must:** describe observable behavior · state the calculation, message, status, response, or persisted value · avoid subjective terms like "works correctly" · avoid repeating the step as the result · include UI/API/data/integration outcomes where relevant · state when no duplicate/side effect occurs.

Prefer step-level expected results when intermediate behavior matters; one final result when only the end outcome matters.
