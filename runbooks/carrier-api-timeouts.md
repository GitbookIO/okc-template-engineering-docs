---
type: Runbook
title: Carrier API timeouts
description: What to do when label purchases fail because a carrier is slow or down.
system: /systems/label-service.md
team: /teams/shipping-core.md
sources:
  - id: incidents-mock-4
    resource: /incidents/mock-4.md
    title: Label purchases failed during a carrier outage
  - id: incidents-mock-3
    resource: /incidents/mock-3.md
    title: Label purchases failed during carrier API timeouts
generated:
  by: workflow:update-runbooks:anthropic/claude-opus-5-5
  at: 2026-11-04T09:00:00Z
stale_after: 2026-12-04T09:00:00Z
verified:
  - by: human:lena@acme.example
    at: 2026-11-06T10:00:00Z
---

## When to use

Label purchases fail for one carrier's services, or for every service while workers wait on one carrier. Customers can't ship.[^incidents-mock-3][^incidents-mock-4]

## Check

1. Look at label purchase errors by carrier. One carrier stands out.
2. Check that carrier's label API response times and status page.
3. Check whether label workers are busy waiting on that carrier.

## Fix

1. Set `labels.carrier_override` to route the failing carrier's services to the backup carrier.[^incidents-mock-3][^incidents-mock-4]
2. If workers are stuck, restart them.[^incidents-mock-3]
3. When the carrier recovers, clear the override.

## Escalate

Tell [Shipping Core](/teams/shipping-core.md) in #team-shipping-core as soon as purchases fail. Tell Payments too if the backup carrier costs more, since customers are charged its price.

## Past incidents

- 4 November 2026: one carrier's outage failed its purchases for 35 minutes.[^incidents-mock-4]
- 24 October 2026: a hanging carrier API failed most purchases for 50 minutes.[^incidents-mock-3]
