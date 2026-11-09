---
type: Pull Request
title: Reject a second entry for the same idempotency key
resource: 'mock://prs/3'
state: merged
number: 88
repository: acme/ledger
author: maya-chen
merged_at: '2026-10-06T16:20:00Z'
issues: [/issues/mock-2.md]
systems: [/systems/ledger.md]
---

The ledger now stores the idempotency key with each charge entry and rejects a second entry with the same key. The second write returns the first entry, so callers can retry safely.

Fixes ENG-219.

## Changed files

- `src/entries/write.ts`
- `migrations/0042_entry_idempotency_key.sql`
