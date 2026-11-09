---
type: Pull Request
title: Store processor response codes on failed charges
resource: 'mock://prs/16'
state: merged
number: 436
repository: acme/billing-api
author: dev-okafor
merged_at: '2026-11-03T15:30:00Z'
systems: [/systems/billing-api.md]
---

Failed charges now keep the processor's response code and message, so support can tell a declined card from a processor error without asking us.

## Changed files

- `src/charges/failure.ts`
- `migrations/0019_charge_failure_code.sql`
