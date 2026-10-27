# Worked Example — Checkout Automation Plan (Reference)

**Owner:** `test-automation-and-frameworks`. A complete worked automation decision for one feature.

## 1. Feature

Guest checkout with a coupon, card payment, and order confirmation. Must run on every release and on Chrome + WebKit.

## 2. Candidate Assessment

| Scenario | Risk | Frequency | Manual cost | Automation cost | Stability | Decision |
|---|---|---|---|---|---|---|
| Coupon calculation | High | Every build | Medium | Low | High | **Automate @ API** |
| Order total / tax | High | Every build | Medium | Low | High | **Automate @ API** |
| Payment decline handling | High | Weekly | High | Medium | Medium | **Automate @ API** + contract |
| Full checkout journey | High | Every release | High | Medium | Medium | **Automate @ E2E (1 case)** |
| Checkout UI responsiveness | Low | Rare | Low | High | Low | **Manual / visual** |
| Payment 3-D Secure challenge | Medium | Rare | Medium | High | Variable | **Manual (provider sandbox)** |

## 3. Test-Level & Tool Choice

- **API:** Playwright `APIRequestContext` for coupon/total/decline (fast, stable, financial).
- **Contract:** Pact between checkout service and payment provider.
- **E2E:** one Playwright journey asserting the *business outcome* (order created + persisted total), not the clicks.
- Not recommended: unit tests owned by engineering for pricing math.

## 4. Framework Structure (excerpt)

```
tests/
  api/        coupon.api.spec.ts   total.api.spec.ts
  e2e/        checkout.e2e.spec.ts
fixtures/     user.fixture.ts      product.fixture.ts
api/          cart.client.ts       order.client.ts
```

## 5. Data, Config, Secrets

- Data via API factories: unique customer `test-user-{timestamp}@example.test`; product seeded per run; cleaned after.
- Config externalized: `BASE_URL`, `ENV`, browser projects (chromium, webkit).
- Card test credentials from the CI secret store — never in code.

## 6. CI/CD

- PR: `tests/api` (sharded ×4) — fast gate.
- Release: `tests/e2e` smoke on deploy.
- Nightly: full regression + cross-browser.

## 7. Flakiness & Diagnostics

- `trace: 'on-first-retry'`, screenshot + video on failure.
- One known flake: WebKit timing on the address autocomplete → replaced fixed `waitForTimeout(2000)` with `await expect(autocomplete).toHaveCount(1)`. Tracked flaky-test rate trending to 0.

## 8. Coverage & ROI

- Critical financial logic covered at API (fast, cheap); one E2E for end-to-end confidence.
- Estimated 6 h implementation, ~1 h/quarter maintenance vs. ~3 h manual per release → positive ROI within a quarter.
- Deliberately **not** automated: 3-D Secure and visual layout (low frequency, high instability, unstable prerequisites).

## 9. Risks / Open Questions

- Payment provider sandbox occasionally slow → may cause environment flakes; monitor.
- Confirm contract-test ownership with the payment team.
