---
type: Pull Request
title: Redact carrier credentials from logs
resource: 'mock://prs/15'
state: merged
number: 152
repository: acme/rates-engine
author: lena-ito
merged_at: '2026-10-18T13:10:00Z'
issues: [/issues/mock-12.md]
systems: [/systems/rates-engine.md]
---

Carrier request logging now drops authorization headers and API key fields. The two exposed keys are rotated.

Fixes ENG-224.

## Changed files

- `src/carriers/logging.ts`
- `test/carriers/logging.test.ts`
