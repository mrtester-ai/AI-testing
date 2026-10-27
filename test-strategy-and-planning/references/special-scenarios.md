# Special Planning Scenarios (Reference)

**Owner:** `test-strategy-and-planning`. These are the highest-value planning overlays — apply the matching scenario to the generic workflow.

## Hotfix / Incident Fix

Optimize for speed without hiding risk. Focus:
1. Reproduce the original problem.
2. Verify the fix.
3. Test the immediate affected area.
4. Test plausible negative scenarios.
5. Test shared components.
6. Execute critical regression.
7. Verify the production deployment where appropriate.

Clearly state what was omitted due to time.

## Security Patch / Platform Upgrade

Consider: installation/deployment · application startup · authentication · authorization · admin · customer functionality · checkout · payment · APIs · integrations · cron/scheduled jobs · search/indexing · cache · sessions · security headers · logs · error handling · critical regression. Validate the vulnerability or affected component when practical and safe.

## Integration Change

Focus: request mapping · response mapping · authentication · authorization · success path · validation failures · timeout · retry · duplicate processing · delayed processing · partial failure · invalid response · recovery · data reconciliation · monitoring and logging.

## UI-Only Change

Do not automatically request full regression. Assess: component reuse · responsive impact · browser impact · accessibility · interaction behavior · journey impact · JavaScript changes · backend/API changes. Use focused regression when evidence supports isolation.

## Critical eCommerce Change

For changes affecting cart, checkout, payment, pricing, promotion, shipping, tax, inventory, or order placement, **increase the default risk level** — failures may affect revenue or order integrity. Include guest and logged-in flows, product types, quantity boundaries, promotions, tax, shipping, payment, order creation, inventory, confirmation, and downstream order processing. See `shared/ecommerce-coverage.md`.
