---
type: Incident
title: Tracking updates delayed by two hours
resource: 'mock://incidents/5'
state: resolved
severity: medium
system: /systems/tracking-events.md
started_at: '2026-10-30T05:00:00Z'
resolved_at: '2026-10-30T07:10:00Z'
---

## What happened

Shipment timelines for one carrier stopped updating for two hours. Customers saw no movement on parcels that were moving.

## Timeline

- 05:00 UTC: the carrier's feed poller starts failing auth.
- 06:50 UTC: support asks why one carrier's parcels look stuck.
- 07:05 UTC: the poller is restarted with a fresh token.
- 07:10 UTC: the backlog of updates is processed.

## Cause

The poller kept retrying with an expired token and nothing alerted on a silent feed. Fixed by refreshing the token on auth errors. An alert is tracked in ENG-235.
