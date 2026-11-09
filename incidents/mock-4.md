---
type: Incident
title: Label purchases failed during a carrier outage
resource: 'mock://incidents/4'
state: resolved
severity: high
system: /systems/label-service.md
started_at: '2026-11-04T07:45:00Z'
resolved_at: '2026-11-04T08:20:00Z'
issues: [/issues/mock-6.md]
---

## What happened

Purchases for one carrier's services failed for 35 minutes. Other carriers kept working.

## Timeline

- 07:45 UTC: the carrier's label API returns errors.
- 07:50 UTC: the 8 second timeout keeps workers free, but those purchases fail.
- 08:15 UTC: `labels.carrier_override` set for that carrier.
- 08:20 UTC: purchases succeed through the backup carrier.

## Cause

The carrier had an outage. Nothing switches carriers on its own yet, so it took a person to set the override.
