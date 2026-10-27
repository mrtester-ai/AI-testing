# Worked Example — Coupon Feature Strategy (Reference)

**Owner:** `test-strategy-and-planning`. A complete worked strategy for one change.

## 1. Executive Summary

**Change:** One-coupon-per-cart discount feature, applied in cart and persisted to the order.
**Objective:** Confirm the discount calculates correctly, applies under the right rules, and persists to the order without corrupting totals.
**Approach:** Risk-based — financial math and persistence at P0 (API + one E2E), rules/boundaries at P1, wording at P3.
**Primary risk:** incorrect monetary calculation or a discount that does not persist to the order.
**Readiness:** not yet assessed.

## 2. Scope

**In:** coupon apply/replace/remove, validity rules (expiry, threshold, single-use), cart total recalculation, persistence to order, guest + logged-in.
**Out:** stacking multiple coupons (not supported this release — risk accepted); third-party coupon affiliate feeds (another team).

## 3. Assumptions & Dependencies

- **Assumption:** only one coupon active at a time (confirmed with product).
- **Dependency:** pricing API available in staging.
- **Unknown:** guest→login cart-merge coupon behavior (clarification raised).

## 4. Risk Assessment

| ID | Risk | Probability | Impact | Priority | Coverage |
|---|---|---|---|---|---|
| R1 | Wrong discount amount | Med | High | P0 | API math cases + E2E assertion |
| R2 | Discount not persisted to order | Med | High | P0 | Order-persistence check + admin verification |
| R3 | Expired/threshold rules wrong | Med | Med | P1 | Decision + boundary cases |
| R4 | Double discount on repeated apply | Low | High | P0 | Idempotency case |

## 5. Test Approach

| Test Type | Scope | Priority | Rationale |
|---|---|---|---|
| API | Math, rules, idempotency | P0/P1 | Fast, stable, financial |
| E2E | One checkout journey | P0 | End-to-end confidence |
| Regression | Cart + checkout + order totals | P0 | Shared pricing logic |
| Exploratory | Coupon + promotions interaction | P2 | Uncertain behavior |

## 6. Regression Strategy

Focused on shared pricing logic: product page price → cart total → checkout total → order total. Chose focused (not full) because the change touches pricing but is isolated to cart/checkout.

## 7. Environment & Test Data

Staging with production-like pricing config; coupons seeded (valid, expired, threshold, single-use); unique customer per run.

## 8. Estimates

| Activity | Scope | Effort | Dependency |
|---|---|---:|---|
| Design | Cases | 3–4 h | Requirements |
| Setup | Data + coupons | 1–2 h | Seed access |
| Execution | API + E2E + regression | 6–8 h | Staging |
| Retest | Post-fix | 2 h | Fix build |

## 9. Entry / Exit Criteria

**Entry:** pricing API available, coupons seeded, requirements testable.
**Exit:** all P0 pass; P1 rules pass; no pricing regression; residual risks documented.

## 10. Residual Risk

Guest→login cart-merge coupon behavior is untested (blocked on clarification). Mitigation: test in production smoke post-deploy; monitor coupon-error rate.

## 11. Release Recommendation

**READY WITH KNOWN RISKS** — P0 pricing/persistence and regression pass; the merge behavior is an accepted, documented risk pending clarification. See `shared/release-readiness.md`.
