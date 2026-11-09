---
type: Runbook
title: Stalled carrier feeds
description: What to do when one carrier's tracking updates stop arriving.
system: /systems/tracking-events.md
team: /teams/platform.md
sources:
  - id: incidents-mock-5
    resource: /incidents/mock-5.md
    title: Tracking updates delayed by two hours
generated:
  by: workflow:update-runbooks:anthropic/claude-opus-5-5
  at: 2026-10-30T07:30:00Z
stale_after: 2026-11-29T07:30:00Z
---

## When to use

Parcels from one carrier look stuck in customers' timelines while they're moving. Support hears it first, since nothing alerts yet.[^incidents-mock-5]

## Check

1. Find when the carrier's feed last sent an update.
2. Look at its poller's logs for repeated auth errors.

## Fix

1. Restart the poller with a fresh token.[^incidents-mock-5]
2. Check that the backlog of updates is processed and timelines catch up.

## Escalate

Tell [Platform](/teams/platform.md) in #team-platform if a feed is silent for more than 20 minutes.

## Past incidents

- 30 October 2026: one carrier's updates were two hours late.[^incidents-mock-5]
