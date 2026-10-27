# Worked Example — Coupon Application in Cart (Reference)

A fully worked design showing techniques, coverage, prioritization, and a written case.

**Owner:** `test-case-design-and-management`.

## 1. Requirement Summary

A guest customer may apply **one** coupon code in the cart. Valid coupons reduce the cart subtotal. A second coupon replaces the first. Invalid, expired, or use-limited coupons are rejected with a specific message. The discount must persist to checkout and the order.

## 2. Assumptions and Clarification Questions

- **Assumption:** only one coupon can be active at a time.
- **Question:** does the coupon survive a cart merge when a guest logs in? (material to expected result — flag to stakeholder)
- **Question:** is the coupon validated again at order placement if it expires mid-checkout?

## 3. Risk Assessment

| Area | Risk | Why |
|---|---|---|
| Discount math / rounding | High | Financial correctness |
| Coupon persistence to order | High | Order integrity |
| Expired / use-limit rules | Medium | Business-rule correctness |
| Message wording | Low | Cosmetic |

## 4. Techniques Selected

- **Equivalence Partitioning** — valid vs. invalid coupon codes.
- **Boundary-Value Analysis** — minimum subtotal threshold for coupon eligibility.
- **Decision-Table Testing** — coupon type × customer type × cart total.
- **State-Transition Testing** — apply → replace → remove.

## 5. Test Cases (extract)

| ID | Title | Req | Priority | Preconditions | Steps | Expected Result |
|---|---|---|---|---|---|---|
| CART-CPN-01 | Valid percentage coupon reduces subtotal | REQ-204 | P0 | Guest cart subtotal = $120; coupon `SAVE10` (10%) active | 1. Add item ($120) 2. Enter `SAVE10` 3. Apply | Subtotal $120, discount −$12, new total $108; discount persists to checkout |
| CART-CPN-02 | Coupon below eligibility threshold rejected | REQ-204 | P1 | Cart subtotal = $40; coupon requires ≥ $50 | 1. Enter eligible-threshold coupon 2. Apply | Error: "This coupon requires a $50 minimum subtotal." No discount applied |
| CART-CPN-03 | Applying a second coupon replaces the first | REQ-205 | P1 | `SAVE10` applied | 1. Enter `SAVE20` 2. Apply | Only `SAVE20` active; discount recalculated; no stacking |
| CART-CPN-04 | Expired coupon rejected | REQ-206 | P0 | Coupon expired yesterday | 1. Enter expired code 2. Apply | Error: "This coupon has expired." Total unchanged |
| CART-CPN-05 | Coupon survives to order and is stored | REQ-207 | P0 | Valid coupon applied | 1. Complete checkout 2. Open order in admin | Order records coupon code and discounted total; persisted amount matches cart |

## 6. Traceability

| Requirement | Risk | Test Case IDs | Coverage Status | Gap |
|---|---|---|---|---|
| REQ-204 coupon applies | High | CART-CPN-01, -02 | Covered | — |
| REQ-205 single coupon | High | CART-CPN-03 | Covered | — |
| REQ-206 expiry | Medium | CART-CPN-04 | Covered | — |
| REQ-207 persistence | High | CART-CPN-05 | Covered | Guest→login merge unexplored |
| REQ-208 login cart-merge behavior | High | — | **Not Covered** | Clarification required |

## 7. Coverage Gaps / Automation

- **Gap:** guest→login cart-merge coupon behavior is blocked on REQ-208 clarification.
- **Automate:** CART-CPN-01, -03, -04 at **API level** (stable, high-frequency, financial). Keep checkout persistence (CART-CPN-05) as one UI/E2E case.

## 8. Release-Critical Checklist

- [ ] P0 coupon math and persistence pass.
- [ ] Expiry and single-coupon rules pass.
- [ ] No double-discount on repeated apply.
