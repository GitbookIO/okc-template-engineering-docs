---
type: Issue
title: Quotes are slow for multi-parcel shipments
resource: 'mock://issues/5'
identifier: ENG-228
state: done
priority: medium
assignee: Ravi Menon
labels: [performance]
system: /systems/rates-engine.md
team: /teams/shipping-core.md
created_at: '2026-10-07T13:00:00Z'
updated_at: '2026-10-13T15:30:00Z'
closed_at: '2026-10-13T15:30:00Z'
---

Quotes for shipments with five or more parcels take 1.4 seconds at p95. The rates engine calls the carrier once per parcel.
