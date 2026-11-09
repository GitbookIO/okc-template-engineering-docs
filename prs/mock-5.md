---
type: Pull Request
title: Partition the delivery queue by shipment
resource: 'mock://prs/5'
state: merged
number: 219
repository: acme/webhooks
author: jonah-park
merged_at: '2026-11-05T16:40:00Z'
issues: [/issues/mock-4.md]
systems: [/systems/webhooks.md]
---

Events are now partitioned by shipment ID. One worker consumes each partition in order, and partitions are spread across the pool, so delivery stays parallel across shipments and ordered within one.

Fixes ENG-226.

## Changed files

- `src/delivery/partition.ts`
- `src/delivery/pool.ts`
- `test/delivery/order.test.ts`
