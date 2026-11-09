---
type: Issue
title: Creating a shipment fails when the address has no postal code
resource: 'mock://issues/10'
identifier: ENG-221
state: done
priority: medium
assignee: Ravi Menon
labels: [bug, api]
system: /systems/shipments-api.md
team: /teams/shipping-core.md
created_at: '2026-10-09T10:30:00Z'
updated_at: '2026-10-15T09:20:00Z'
closed_at: '2026-10-15T09:20:00Z'
---

POST /v1/shipments returns a 500 when the destination has no postal code, which is valid in some countries. It should accept those addresses, and return a 422 with a clear message when a postal code is required but missing.
