---
type: Pull Request
title: Cap delivery retries at 5 attempts
resource: 'mock://prs/6'
state: merged
number: 211
repository: acme/webhooks
author: tomas-silva
merged_at: '2026-10-30T11:00:00Z'
systems: [/systems/webhooks.md]
---

A failed delivery is now retried 5 times over about 2 hours, then dropped and shown as failed. Endpoints that stay down for a day were filling the queue. Agreed in #eng-platform on 17 October.

## Changed files

- `src/delivery/retry.ts`
- `config/retry.yaml`
