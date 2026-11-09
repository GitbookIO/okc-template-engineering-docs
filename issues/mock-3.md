---
type: Issue
title: Invoice PDFs show charge times in UTC
resource: 'mock://issues/3'
identifier: ENG-231
state: backlog
priority: low
labels: [bug]
system: /systems/billing-api.md
team: /teams/payments.md
created_at: '2026-11-03T10:15:00Z'
updated_at: '2026-11-03T10:15:00Z'
---

Customers outside UTC see label charges on the wrong day near midnight. The PDF should use the account's time zone.
