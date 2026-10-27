# Worked Example — QA Status Report, Risk, and Escalation (Reference)

**Owner:** `quality-leadership-and-communication`.

## QA Status Report (worked)

> **Executive assessment:** Checkout is release-ready with one accepted residual risk. All P0 financial and order journeys pass; a carrier-integration gap is documented.
>
> **Evidence:** P0 100% executed/passed · checkout E2E passed on Chrome + WebKit · regression on pricing/cart/checkout/order passed · one P2 Safari layout issue (no functional impact).
>
> **Risks and gaps:** (1) Carrier X integration untested — its test environment is unavailable. (2) Guest→login cart-merge coupon behavior unverified (clarification pending).
>
> **Recommendation:** READY WITH KNOWN RISKS — proceed; validate Carrier X via production smoke and monitor failed shipping requests.
>
> **Owners and next steps:** QA — production smoke post-deploy. Product — resolve merge-behavior clarification. Platform — restore Carrier X test env.
>
> **Decision required:** Release owner to explicitly accept the untested-carrier risk before deploy.

Bad version (activity only, no confidence):
> "We executed 96% of tests with a 98% pass rate."
Without saying what failed or remained untested.

## Risk Communication

Format: **Risk → Impact → Evidence → Mitigation → Decision**.

> **Risk:** Shipping-method regression has not been fully tested — the carrier test environment is unavailable.
> **Impact:** Customers using this carrier could hit checkout or fulfilment problems.
> **Evidence:** Other shipping methods passed; carrier-specific integration testing remains blocked.
> **Mitigation:** Run production smoke immediately post-deploy and monitor failed shipping requests.
> **Decision:** Release owner should explicitly accept the untested carrier-integration risk before deployment.

## Escalation Message

Format: problem · impact · evidence · blocker · options · recommended option · decision required · timing.

> **Problem:** Checkout cannot be fully validated — the payment sandbox rejects all test cards.
> **Impact:** Payment success/failure paths are unverified; release confidence for checkout is low.
> **Evidence:** 5/5 attempts return `sandbox_unavailable`; other flows pass.
> **Blocker:** Payment provider sandbox outage (open 6 h).
> **Options:** (A) delay release until sandbox restored; (B) release with card flows untested + post-deploy verification; (C) use the provider's secondary sandbox.
> **Recommended:** (C), falling back to (A) if (C) is unavailable.
> **Decision required:** Release owner, before the 16:00 cut-off.
> **Timing:** Needs a decision within the hour to keep the release window.
