# RCA Techniques and Regression Analysis (Reference)

**Owner:** `defect-management-and-root-cause-analysis`.

## Five Whys

For problems with a relatively clear causal chain. Do not force exactly five questions — stop when a useful, evidence-supported underlying cause is reached.

## Change Analysis

Compare: last working version · first failing version · code changes · configuration · dependency · infrastructure · feature flags · data. Useful for regression investigation.

## Timeline Reconstruction

For intermittent issues, distributed systems, integration issues, async processing, and production incidents — build a chronological sequence from timestamps across systems.

## Log and Trace Correlation

Use request ID · correlation ID · order ID · customer ID · transaction ID · message ID to follow a transaction across components.

## Fishbone Analysis

Categories: code · configuration · data · environment · integration · process · requirements · monitoring · test coverage. Use when multiple contributing factors may exist.

## Fault-Tree Analysis

Use for complex or high-impact failures where several conditions could independently or jointly produce the outcome.

## Root Cause Confidence

- **Confirmed:** direct evidence demonstrates the causal relationship.
- **Likely:** strong supporting evidence, complete confirmation unavailable.
- **Possible:** plausible explanation requiring further investigation.
- **Unknown:** insufficient evidence.

Never present Likely/Possible as confirmed.

## Regression Analysis

After a fix, determine what the change could have affected:

- **Direct** — the exact functionality changed.
- **Adjacent** — closely related functionality sharing a component, validation, rule, data, control, or API.
- **Integration** — affected upstream/downstream integrations.
- **Historical** — related previous defects or historically unstable functionality.
- **Critical-journey** — when a high-risk shared component changed.

Choosing scope: a fix to shared pricing logic may need validation across product page, cart, checkout, order, invoice, and refund. Do **not** run full regression for every defect — scope by change impact and risk.
