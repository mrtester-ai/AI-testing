# eCommerce Coverage (Shared Reference)

Single canonical eCommerce coverage checklist.

**Owned by:** `test-strategy-and-planning`.
**Linked from:** `test-case-design-and-management`, `web-api-and-integration-testing`, `defect-management-and-root-cause-analysis`, `quality-leadership-and-communication`.

Apply only the areas relevant to the change and its risk; do not treat this as a mandatory full-regression list.

## Customer

Guest · logged-in · different customer groups · new vs. existing customer.

## Catalog and Product

Product types (simple, configurable, bundle, grouped, virtual, downloadable) · options and required selections · price, special price, discounts, coupons, tax, currency, rounding · availability and inventory · minimum/maximum quantity · stock, backorder, reservation.

## Cart and Wishlist

Add / update / remove · quantity boundaries · promotions and free gifts · cart total · persistence · wishlist guest vs. logged-in behavior · authentication transition · counter.

## Checkout

Guest and logged-in checkout · address · shipping methods and restrictions · store pickup / Click & Collect · tax · promotions and coupons · payment · order review · submission · validation.

## Payment

Success · decline · failure · timeout · retry · duplicate submission · cancellation · authentication challenges (e.g. 3-D Secure) · final transaction state.

## Order and Post-Order

Order creation and number · customer · items · quantity · price · discount · tax · shipping · total · payment status · fulfilment info. Then: invoice · shipment · cancellation · refund · credit memo · customer notification.

## Integrations

Payment gateway · ERP · OMS · CRM · warehouse · shipping providers · tax services · search · CMS · customer platforms · analytics. Validate **both success and failure paths**.

## Cross-System Validation Chain

For transaction-critical operations, verify consistency across every participating layer — do not trust the storefront confirmation alone:

Storefront → Checkout API → Payment → Order → Inventory → Order Management / ERP → Fulfilment → Customer notification

**Rule:** a correct screen does not mean downstream data is correct. Verify persistence, not just UI.

## Highest-Risk Areas

Treat changes to **cart, checkout, payment, pricing, promotion, shipping, tax, inventory, or order placement** as elevated risk — failures may affect revenue or order integrity.
