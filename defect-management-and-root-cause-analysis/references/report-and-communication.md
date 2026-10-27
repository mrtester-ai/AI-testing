# Defect Reporting and Communication (Reference)

**Owner:** `defect-management-and-root-cause-analysis`.

## Defect Report Template

**Title** — `[Area] + [Trigger/Condition] + [Observable Failure]`.
> Good: "Checkout — guest is redirected to login and loses the product when adding to Wishlist."
> Avoid: "Wishlist issue", "Checkout bug".

**Environment** — environment · build/version · browser/device · account/customer type · relevant configuration.

**Preconditions** — user state · product/data state · configuration · permissions · feature flags · existing records.

**Steps to Reproduce** — start from a defined state · minimum actions · explicit data where important · stop where the failure is observable.

**Expected Result** / **Actual Result** — objective required behavior vs exact observed behavior (include exact messages/codes).

**Impact** — customer · business · data · operational · scope · workaround.

**Reproducibility** — e.g. `5/5 attempts` or `Intermittent: 2/5`.

**Severity** / **Priority** — state with justification (see `shared/severity-and-priority.md`).

**Evidence** — screenshot/video · API request/response · console · logs · timestamp · correlation ID · test data.

## Jira Communication Standards

- Lead with the outcome.
- State what was tested and the observed result.
- Include evidence when relevant.
- Mention limitations only when they affect confidence.
- Avoid unnecessary technical speculation.
- Use collaborative language.

> Prefer: "The issue is still reproducible on staging. The selected pickup store is correct during checkout, but the order confirmation shows a different store. Please investigate the persisted store data used by confirmation."
> Avoid: "This still doesn't work. Backend issue. Please fix."

## Validation Comment Examples

- **Pass:** "Retested on the latest staging build. No longer reproducible; expected behavior displays correctly. Targeted regression on the related flow also passed."
- **Fail:** "Retested on the latest staging build, but still reproducible. Expected behavior not met; the ticket should remain open."
- **Partial pass:** "Resolved for the primary scenario, but the same problem still occurs under the alternate condition below. The fix is only partially validated."
- **Blocked:** "Validation is blocked because the required test configuration is unavailable in the test environment. The fix cannot be confirmed until this dependency is restored."

## Defect Pattern Analysis

Classify multiple defects by: component · root cause · requirement gap · test-coverage gap · integration · environment · configuration · data · escape stage · severity · recurrence. Look for trends (repeated validation defects, repeated integration mapping problems, recurring checkout regressions, missing boundary coverage, environment config problems, repeated production escapes from the same component). **Do not infer a systemic pattern from a single defect.**

## Preventive Actions

Recommend based on confirmed causes and recurring evidence:

- **Code:** validation · error handling · remove duplicated logic · idempotency.
- **Automated testing:** unit · API regression · integration · E2E · boundary coverage (prefer the lowest reliable layer).
- **Manual testing:** targeted regression scenario · exploratory charter · release smoke.
- **Requirements:** clarify acceptance criteria · document boundary behavior · define error handling.
- **Monitoring:** structured logging · alerts · failed-request tracking · transaction tracing.
- **Process:** regression-impact review · code-review checklist · integration contract validation · test-data management.

Preventive actions must address the cause or the escape mechanism — not merely add more test cases.
