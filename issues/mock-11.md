---
type: Issue
title: List shipments ignores the status filter after the first page
resource: 'mock://issues/11'
identifier: ENG-238
state: in progress
priority: medium
assignee: Ravi Menon
labels: [bug, api]
system: /systems/shipments-api.md
team: /teams/shipping-core.md
created_at: '2026-11-04T10:00:00Z'
updated_at: '2026-11-06T16:00:00Z'
---

GET /v1/shipments?status=delivered returns delivered shipments on the first page, then every status on the pages after it. The cursor doesn't carry the filter.
