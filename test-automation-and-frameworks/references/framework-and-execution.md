# Framework Design and Execution (Reference)

**Owner:** `test-automation-and-frameworks`.

## Separations

A maintainable framework separates: **tests · configuration · test data · fixtures · page/component abstractions · API clients · helpers/utilities · reporting · environment management.**

Create an abstraction only when it removes meaningful duplication or improves maintainability. Avoid excessive abstraction.

## Example Structure (Playwright)

```
tests/
  smoke/        regression/     e2e/        api/
pages/
  login.page    product.page    cart.page   checkout.page
fixtures/
  user.fixture  product.fixture order.fixture
api/
  customer.client  cart.client  order.client
data/
  customers     products        addresses
utils/
  assertions    helpers
```

Configuration stays separate from test behavior. Adapt to project complexity.

## Configuration — Externalize

Base URLs · browser config · environment names · feature flags · service endpoints · test accounts. Never scatter environment-specific values through the suite.

## Test Data

Approaches: API-generated data · authorized DB seed · fixtures · factories · unique generated identifiers · dedicated accounts · environment reference data.

Data should be predictable · reproducible · safe · isolated where practical · easy to clean up. Avoid dependencies on shared records. For unique resources generate predictable uniqueness (`test-user-{timestamp}@example.test`) and ensure cleanup to avoid uncontrolled accumulation.

## Secrets

Never hard-code: passwords · API keys · access/refresh tokens · private certificates · real payment credentials.

Use the CI/CD secret store (GitHub Actions secrets, Azure DevOps variables, Azure Key Vault, GitLab CI/CD variables). Prevent secrets appearing in logs, screenshots, traces, reports, or source control.

## Selector Strategy

Preference order:
1. User-facing accessible roles and names
2. Explicit test identifiers
3. Stable semantic attributes
4. Stable CSS when necessary

Avoid: deep DOM hierarchy · generated class names · position · dynamic IDs · frequently changing text.

## Code Example (Playwright, TypeScript)

```typescript
import { test, expect } from '@playwright/test';

test('place order with a valid card', async ({ page }) => {
  await page.goto('/cart');
  await page.getByRole('button', { name: 'Checkout' }).click();
  await page.getByLabel('Card number').fill('4111 1111 1111 1111');
  await page.getByRole('button', { name: 'Place Order' }).click();

  await expect(page.getByRole('heading', { name: 'Order confirmed' })).toBeVisible();
  await expect(page.getByTestId('order-total')).toHaveText('$108.00');
});
```

```typescript
import { test, expect } from '@playwright/test';

test('rejects an expired coupon at the API layer', async ({ request }) => {
  const res = await request.post('/api/cart/coupon', {
    data: { code: 'EXPIRED10' },
  });
  expect(res.status()).toBe(422);
  expect(await res.json()).toMatchObject({ error: 'coupon_expired' });
});
```

Note: UI test asserts the business outcome (confirmation + total), not just that a button was clicked; the API test asserts the contract at the lowest reliable level.
