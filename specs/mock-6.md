---
type: Spec
title: Cursor pagination for list shipments
resource: 'mock://specs/6'
kind: tdd
state: approved
author: Lena Ito
systems: [/systems/shipments-api.md]
approved_at: '2026-10-09T14:00:00Z'
---

## Design

- GET /v1/shipments pages with an opaque cursor.
- The default page size is 50 and the maximum is 200.
- Filters given on the first request apply to every page.
- Offset pagination keeps working until v1 is retired.
