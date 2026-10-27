# Severity and Priority (Shared Reference)

Canonical severity, priority, and impact definitions.

**Owned by:** `defect-management-and-root-cause-analysis`.
**Linked from:** `test-case-design-and-management`, `test-strategy-and-planning`, `quality-leadership-and-communication`.

Do not restate these scales in other skills — link here instead.

## Severity (impact of the failure)

Use the team's official classification when provided; otherwise use this default.

| Level | Examples |
|---|---|
| **Critical / S1** | Critical customer journey unavailable; checkout broadly down; payment causes financial risk; data corruption/loss; serious security exposure; production unavailable; no practical workaround. |
| **High / S2** | Major functionality unavailable; significant customer group affected; important integration broken; incorrect order/price/tax/promotion/inventory; serious issue with a workaround. |
| **Medium / S3** | Secondary functionality affected; limited customer impact; practical workaround exists; incorrect behavior in a non-critical journey. |
| **Low / S4** | Cosmetic defect; minor alignment; low-impact text issue; minor usability problem with no functional impact. |

Severity is **not** based on technical complexity. A one-line code defect can be Critical; a complex engineering issue can be Low.

## Priority (urgency of resolution)

| Level | Meaning |
|---|---|
| **P0** | Immediate action required. |
| **P1** | Addressed before the targeted release unless risk is explicitly accepted. |
| **P2** | Important but schedulable against release priorities. |
| **P3** | Low urgency or backlog. |

Consider: release timing, customer exposure, business commitments, revenue impact, frequency, workaround, regulatory requirements, dependencies.

## Severity ≠ Priority

The same failure can carry different severity and priority.

> A serious defect in an unreleased, feature-flagged-off capability may be **High severity** but **P3 priority**.

## Impact Assessment

Evaluate across all of these:

- **Customer impact:** who is affected — guest, logged-in, specific groups, all?
- **Business impact:** revenue, conversion, order placement, payment, fulfilment, support, operations, compliance.
- **Data impact:** incorrect, missing, duplicate, corrupted, or unsynchronized data; recovery needs.
- **Scope:** one environment / browser / device / customer / product / config / integration, or all users and multiple systems.
- **Workaround:** none / manual / customer / configuration / operational.

Do not lower impact solely because a workaround exists — judge how practical and safe it is.
