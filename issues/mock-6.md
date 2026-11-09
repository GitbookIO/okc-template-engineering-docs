---
type: Issue
title: Add a circuit breaker for carrier label calls
resource: 'mock://issues/6'
identifier: ENG-233
state: in progress
priority: high
assignee: Ravi Menon
labels: [reliability]
system: /systems/label-service.md
team: /teams/shipping-core.md
created_at: '2026-10-25T09:00:00Z'
updated_at: '2026-11-04T10:00:00Z'
---

When a carrier's label API slows down, every label purchase waits on it. The 8 second timeout helps, but we keep calling a carrier that is clearly down.

Stop calling a carrier after repeated failures and fail fast, or switch to a backup carrier if one is set.

## Notes

- Ravi: the 4 November outage is a second case. Failover design is in review.
