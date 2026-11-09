---
type: Pull Request
title: Cache carrier rates for an hour
resource: 'mock://prs/7'
state: merged
number: 157
repository: acme/rates-engine
author: lena-ito
merged_at: '2026-10-29T09:30:00Z'
systems: [/systems/rates-engine.md]
---

The rate cache now keeps carrier rates for 60 minutes instead of 15. That cuts carrier rate calls by about 70 percent. Price-change notices from carriers still clear the cache for that carrier right away.

## Changed files

- `src/cache/rates.ts`
- `config/cache.yaml`
