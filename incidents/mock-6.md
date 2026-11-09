---
type: Incident
title: Shipments API errors after a deploy
resource: 'mock://incidents/6'
state: resolved
severity: medium
system: /systems/shipments-api.md
started_at: '2026-11-02T15:05:00Z'
resolved_at: '2026-11-02T15:25:00Z'
---

## What happened

About a third of shipment creates returned a 500 for 20 minutes.

## Timeline

- 15:05 UTC: the deploy with a new migration goes out.
- 15:10 UTC: error rate alert fires.
- 15:20 UTC: the deploy is rolled back.
- 15:25 UTC: errors stop.

## Cause

The migration added a required column with no default, so inserts from old instances failed during the rollout. Rerun the next day with a default value.
