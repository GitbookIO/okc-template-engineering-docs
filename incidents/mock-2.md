---
type: Incident
title: Webhook deliveries fell 40 minutes behind
resource: 'mock://incidents/2'
state: resolved
severity: high
system: /systems/webhooks.md
started_at: '2026-10-14T18:10:00Z'
resolved_at: '2026-10-14T19:05:00Z'
---

## What happened

Customers got tracking webhooks up to 40 minutes late during the evening peak.

## Timeline

- 18:10 UTC: queue depth starts growing.
- 18:30 UTC: alert fires at 10,000 queued events.
- 18:45 UTC: a second consumer is started by hand.
- 19:05 UTC: the queue is drained.

## Cause

A carrier sent three times its usual volume of tracking updates and a single consumer couldn't keep up. Fixed by moving delivery to a worker pool.
