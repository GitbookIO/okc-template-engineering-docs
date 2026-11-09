---
type: Pull Request
title: Deliver retries from a parallel worker pool
resource: 'mock://prs/4'
state: merged
number: 203
repository: acme/webhooks
author: jonah-park
merged_at: '2026-10-16T13:00:00Z'
systems: [/systems/webhooks.md]
---

Retries now go through a pool of 16 workers instead of a single queue consumer. On 14 October one consumer couldn't keep up with a burst of tracking updates and deliveries fell 40 minutes behind.

## Changed files

- `src/delivery/pool.ts`
- `src/delivery/consumer.ts`
