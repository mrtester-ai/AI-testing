# Worked Example — Wrong Pickup Store on Confirmation (Reference)

**Owner:** `defect-management-and-root-cause-analysis`. A complete worked RCA and fix validation.

## 1. Defect Summary

Order confirmation displays a different pickup store than the one selected during checkout.

## 2. Expected vs Actual

| Expected | Actual |
|---|---|
| Confirmation shows the store selected at checkout and persisted to the order | Confirmation shows a different (stale) store |

## 3. Reproduction Conditions

Staging, build `2026.10.3`, Chrome; guest checkout; product with store-pickup enabled; reproducibility **5/5**.

## 4. Impact

Customer may collect from the wrong store. Business: fulfilment/support cost. Scope: all store-pickup orders. Workaround: none practical.

## 5. Evidence

Cart shows Store A → checkout shows Store A → `GET /orders/8842` returns `store: "A"` → confirmation page displays Store B. Correlation ID `c1a9…`.

## 6. Investigation Findings

- **Confirmed:** the order record persists the correct store (A).
- **Confirmed:** the confirmation view renders store B.
- **Hypothesis:** the confirmation reads store data from the cart/session rather than the order.
- **Unknown:** whether a cache layer serves a stale confirmation fragment.

## 7. Root Cause

- **Symptom:** confirmation shows the wrong store.
- **Trigger:** customer changes the selected store during checkout.
- **Root cause:** confirmation data is populated from stale cart store data rather than the final order fulfilment data. **Confidence: Confirmed.**
- **Escape cause:** existing regression validates store selection during checkout but never validates the persisted store on the final order.

## 8. Fix Validation

- Original reproduction re-run on build `2026.10.4`: confirmation now shows Store A. **PASS.**
- Variations: change store mid-checkout, multiple stores, guest + logged-in — all pass.
- Targeted regression: checkout store selection, order persistence, confirmation, invoice store.
- Side effects: none observed.

## 9. Residual Risk

Confirmation fragment caching was not fully reproduced; mitigated by production smoke + monitoring of confirmation render errors.

## 10. Recommendation

Close the defect. Raise a follow-up preventive task: add an automated E2E assertion comparing checkout selection, persisted order store, and confirmation output.
