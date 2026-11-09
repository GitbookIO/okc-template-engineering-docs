---
type: Issue
title: Tracking webhooks arrive out of order
resource: 'mock://issues/4'
identifier: ENG-226
state: done
priority: high
assignee: Jonah Park
labels: [bug, webhooks]
system: /systems/webhooks.md
team: /teams/platform.md
created_at: '2026-10-22T08:30:00Z'
updated_at: '2026-11-05T17:00:00Z'
closed_at: '2026-11-05T17:00:00Z'
---

Two customers report getting "delivered" before "out for delivery" for the same shipment. It started after retries moved to the parallel worker pool.

Customers build their own timelines from our events, so order matters to them.

## Notes

- Jonah: fixed by partitioning the delivery queue by shipment, see #eng-platform.
