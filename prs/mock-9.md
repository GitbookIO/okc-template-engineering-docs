---
type: Pull Request
title: Time out carrier label calls after 8 seconds
resource: 'mock://prs/9'
state: merged
number: 96
repository: acme/label-service
author: ravi-menon
merged_at: '2026-10-26T10:20:00Z'
issues: [/issues/mock-6.md]
systems: [/systems/label-service.md]
---

Label purchases now give up on a carrier call after 8 seconds and return a retryable error. On 24 October calls hung for 60 seconds and used up every worker thread.

Part of ENG-233. The circuit breaker comes next.

## Changed files

- `src/carriers/client.ts`
- `config/timeouts.yaml`
