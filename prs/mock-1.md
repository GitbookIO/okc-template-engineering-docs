---
type: Pull Request
title: Add idempotency keys to charge requests
resource: 'mock://prs/1'
state: merged
number: 412
repository: acme/billing-api
author: dev-okafor
merged_at: '2026-10-20T14:12:00Z'
issues: [/issues/mock-1.md]
systems: [/systems/billing-api.md]
---

Every charge request now carries an idempotency key built from the label purchase ID. A retry reuses the key, so the processor returns the first result instead of charging again.

Fixes ENG-214. Follows the Idempotent charges RFC.

## Changed files

- `src/charges/create.ts`
- `src/charges/idempotency.ts`
- `test/charges/retry.test.ts`
