---
type: Pull Request
title: Retry failed charges with a fixed delay
resource: 'mock://prs/2'
state: merged
number: 431
repository: acme/billing-api
author: dev-okafor
merged_at: '2026-10-27T10:05:00Z'
systems: [/systems/billing-api.md]
---

Failed charges are now retried 3 times, 10 seconds apart, then marked failed. With exponential backoff, a charge could stay pending for several minutes, and support asked for a faster answer when a card is declined.

Retries still reuse the idempotency key.

## Changed files

- `src/charges/retry.ts`
- `test/charges/retry.test.ts`
