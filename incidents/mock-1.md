---
type: Incident
title: Customers charged twice for one label
resource: 'mock://incidents/1'
state: resolved
severity: critical
system: /systems/billing-api.md
started_at: '2026-10-02T08:55:00Z'
resolved_at: '2026-10-02T10:30:00Z'
issues: [/issues/mock-1.md, /issues/mock-2.md]
---

## What happened

Fourteen accounts were charged twice for single label purchases. Their ledger balances moved twice too.

## Timeline

- 08:55 UTC: the card processor starts timing out.
- 09:20 UTC: support reports double charges.
- 09:35 UTC: the charge retry job is paused.
- 10:30 UTC: duplicate ledger entries removed, refunds issued.

## Cause

Our retry job and the processor's own retry both charged the card after a timeout, and the ledger recorded both charges. Fixed for good by idempotency keys on charges and in the ledger.
