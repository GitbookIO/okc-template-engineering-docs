---
type: Runbook
title: Duplicate charges
description: What to do when customers are charged twice for one label.
system: /systems/billing-api.md
team: /teams/payments.md
sources:
  - id: incidents-mock-1
    resource: /incidents/mock-1.md
    title: Customers charged twice for one label
generated:
  by: workflow:update-runbooks:anthropic/claude-opus-5-5
  at: 2026-10-02T11:00:00Z
stale_after: 2026-11-01T11:00:00Z
---

## When to use

Customers write in about two charges for one label, or the ledger shows a balance moving twice for one purchase. It has happened while the card processor was timing out.[^incidents-mock-1]

## Check

1. Find charges that share a label purchase ID in the last hour.
2. Check whether the card processor is timing out.
3. Look for two ledger entries for one charge.

## Fix

1. Pause the charge retry job.[^incidents-mock-1]
2. Refund the duplicate charges.[^incidents-mock-1]
3. Remove the duplicate ledger entries, keeping the first one.[^incidents-mock-1]

## Escalate

Tell [Payments](/teams/payments.md) in #team-payments right away. Any double charge is customer money.

## Past incidents

- 2 October 2026: fourteen accounts charged twice after processor timeouts.[^incidents-mock-1]
