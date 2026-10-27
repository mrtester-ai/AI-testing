# Test-Design Techniques (Shared Reference)

The canonical catalogue of test-design techniques, when to use each, and a worked example.

**Owned by:** `test-case-design-and-management`.
**Linked from:** `quality-leadership-and-communication` (coaching), `web-api-and-integration-testing` (application at the interface level), `test-strategy-and-planning` (choosing techniques by risk).

## Selection Table (behavior → technique)

| If the behavior involves… | Use |
|---|---|
| A range of inputs that behave the same | Equivalence Partitioning |
| Minimum, maximum, threshold, quantity, length, date, price, capacity | Boundary-Value Analysis |
| Outcomes depending on combinations of rules/conditions | Decision-Table Testing |
| Behavior that depends on current state or previous actions | State-Transition Testing |
| Many independent configuration dimensions | Pairwise / Combinatorial Testing |
| A complete end-to-end customer journey | Scenario / Use-Case Testing |
| Uncertainty, poor specification, or high-risk areas | Exploratory Testing (charter) |

Choose techniques based on the problem. **Do not apply every technique mechanically.**

## Equivalence Partitioning

Divide a range of inputs into groups expected to behave similarly.

*Partitions:* valid · invalid · empty · unsupported format · unauthorized.

> **Example:** Quantity 1–100. Partitions: &lt;1 (invalid), 1–100 (valid), &gt;100 (invalid) → 3 tests, not 100.

## Boundary-Value Analysis

Test just inside, on, and just outside each boundary.

For valid range `1`–`100`: `0`, `1`, `2`, `99`, `100`, `101`. Add extreme values only when they carry real business/technical risk.

## Decision-Table Testing

For outcomes driven by rule combinations — promotions, shipping selection, tax, payment availability, permissions, stock, free gifts, approval workflow.

Cover each meaningful combination; avoid duplicating rows that yield the same outcome.

> **Example:** Free shipping when (order ≥ $50) AND (domestic). Four rows cover the conditions/outcomes; drop rows that collapse to the same result.

## State-Transition Testing

For behavior that changes with state — order status, payment status, account status, subscription, cart, authentication, retry/lockout.

Verify **valid** transitions, **invalid** transitions, **repeated** transitions, and **recovery** transitions.

## Pairwise / Combinatorial Testing

Use when many dimensions exist and exhaustive combinations are impractical (browser × device × customer type × payment × shipping × currency × product type).

**Exception:** never pairwise-reduce combinations already known to be individually high-risk — cover those explicitly.

## Scenario / Use-Case Testing

For complete journeys. Verify entry point · main success path · alternate path · failure path · recovery path · final persisted state · notifications and downstream effects.

## Exploratory Testing (Charter)

For uncertain, complex, or high-risk areas where scripted tests create false confidence.

**Charter template:**
- **ID / Title:**
- **Mission:**
- **Scope:**
- **Primary risks:**
- **Test ideas:**
- **Test data:**
- **Environment / tools:**
- **Timebox:**
- **Evidence to capture:**
- **Exit condition:**
- **Findings / follow-up:**
