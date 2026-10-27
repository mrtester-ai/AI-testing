# Worked Example — Coupon Apply at the API (Reference)

**Owner:** `web-api-and-integration-testing`. A worked API/integration example showing persistence and downstream verification.

## 1. Scenario

Guest applies coupon `SAVE10` in the cart. Expect the subtotal discount applied, persisted to the cart, and carried to the order on checkout.

## 2. Interfaces and Boundaries

| Layer | Component | Input | Expected output | Evidence |
|---|---|---|---|---|
| UI | Cart page | Enter coupon, click Apply | `POST /api/cart/coupon` | Browser network |
| API | Cart service | `{ code: "SAVE10" }` | `200` + `{ discount, total }` | API response |
| Data | Cart persistence | Processed data | Cart stores coupon + discounted total | `GET /api/cart` |
| Integration | Order service | On checkout | Order records coupon + discounted total | Order record |

## 3. Test Cases

| ID | Scenario | Layer | Priority | Steps | Expected |
|---|---|---|---|---|---|
| CPN-API-01 | Valid coupon applies | API | P0 | POST `/cart/coupon` `SAVE10` | `200`; `discount=12`; `total=108` |
| CPN-API-02 | Below threshold rejected | API | P1 | POST with coupon requiring ≥$50 on a $40 cart | `422`; `error=coupon_threshold`; total unchanged |
| CPN-API-03 | Expired rejected | API | P0 | POST expired code | `422`; `error=coupon_expired` |
| CPN-API-04 | Second coupon replaces first | API | P1 | Apply `SAVE10`, then `SAVE20` | Only `SAVE20` active; recalced total |
| CPN-API-05 | Persistence | API+Data | P0 | Apply, then `GET /cart` | Cart returns coupon `SAVE10` and discounted total |
| CPN-API-06 | Persists to order | Integration | P0 | Apply → checkout → `GET /orders/{id}` | Order stores coupon and discounted total |
| CPN-API-07 | Idempotent double submit | API | P0 | POST same request twice | No double discount; single coupon |

## 4. Evidence (example)

**Request:** `POST /api/cart/coupon` · body `{"code":"SAVE10"}` · `X-Correlation-Id: 8f3a…`
**Response:** `200` · `{"discount":12,"total":108}`
**Persistence:** `GET /api/cart` → `{"coupon":"SAVE10","total":108}`
**Downstream:** `GET /orders/10231` → `{"coupon":"SAVE10","total":108}`

## 5. Findings & Gaps

- Observed: `SAVE10` on a $40 cart returns `200` with `discount:0` instead of `422`. **Observation**, not a stated root cause — needs classification against the contract.
- Gap: guest→login cart merge not covered (blocked on clarification).
- Recommendation: add an automated contract check for the coupon error schema.
