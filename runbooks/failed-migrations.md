---
type: Runbook
title: Failed migrations
description: What to do when a deploy's database migration breaks requests.
system: /systems/shipments-api.md
team: /teams/shipping-core.md
sources:
  - id: incidents-mock-6
    resource: /incidents/mock-6.md
    title: Shipments API errors after a deploy
generated:
  by: workflow:update-runbooks:anthropic/claude-opus-5-5
  at: 2026-11-02T15:45:00Z
stale_after: 2026-12-02T15:45:00Z
---

## When to use

Errors jump right after a deploy that includes a migration, while old and new instances run side by side.[^incidents-mock-6]

## Check

1. Match the start of the errors to the deploy time.
2. Look for insert errors that name a new column.

## Fix

1. Roll the deploy back.[^incidents-mock-6]
2. Change the migration so new columns have a default or allow nulls, then deploy again.[^incidents-mock-6]

## Escalate

Tell [Shipping Core](/teams/shipping-core.md) in #team-shipping-core before rolling back a deploy that's still in progress.

## Past incidents

- 2 November 2026: a third of shipment creates failed for 20 minutes.[^incidents-mock-6]
