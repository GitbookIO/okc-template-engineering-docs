---
type: Incident
title: Label purchases failed during carrier API timeouts
resource: 'mock://incidents/3'
state: resolved
severity: critical
system: /systems/label-service.md
started_at: '2026-10-24T13:20:00Z'
resolved_at: '2026-10-24T14:10:00Z'
issues: [/issues/mock-6.md]
---

## What happened

Most label purchases failed for 50 minutes. Customers couldn't ship.

## Timeline

- 13:20 UTC: one carrier's label API slows to 60 second responses.
- 13:30 UTC: every label worker is waiting on that carrier.
- 13:55 UTC: `labels.carrier_override` set to route that carrier's services to the backup carrier.
- 14:10 UTC: workers restarted, purchases succeed.

## Cause

Label calls had no timeout, so one slow carrier used up every worker thread. Fixed by an 8 second timeout. A circuit breaker is tracked in ENG-233.
