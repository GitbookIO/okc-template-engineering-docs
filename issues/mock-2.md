---
type: Issue
title: Ledger accepts two entries for one charge
resource: 'mock://issues/2'
identifier: ENG-219
state: done
priority: high
assignee: Maya Chen
labels: [bug, payments]
system: /systems/ledger.md
team: /teams/payments.md
created_at: '2026-10-02T11:20:00Z'
updated_at: '2026-10-06T16:40:00Z'
closed_at: '2026-10-06T16:40:00Z'
---

The ledger writes one entry per charge attempt that succeeds at the processor. When a charge succeeds twice, the balance moves twice.

The ledger should refuse a second entry for the same charge, whatever the billing side does.
