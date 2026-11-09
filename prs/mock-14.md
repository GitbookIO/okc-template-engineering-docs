---
type: Pull Request
title: Add cursor pagination to list shipments
resource: 'mock://prs/14'
state: merged
number: 548
repository: acme/shipments-api
author: lena-ito
merged_at: '2026-10-22T16:00:00Z'
systems: [/systems/shipments-api.md]
---

GET /v1/shipments now pages with an opaque cursor. The default page size is 50 and the maximum is 200. Offset pagination still works until v1 is retired.

## Changed files

- `src/shipments/list.ts`
- `src/pagination/cursor.ts`
