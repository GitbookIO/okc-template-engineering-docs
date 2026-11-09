---
type: Issue
title: Label charges retried twice after a processor timeout
resource: 'mock://issues/1'
identifier: ENG-214
state: done
priority: high
assignee: Dev Okafor
labels: [bug, payments]
system: /systems/billing-api.md
team: /teams/payments.md
created_at: '2026-10-02T09:40:00Z'
updated_at: '2026-10-20T15:05:00Z'
closed_at: '2026-10-20T15:05:00Z'
---

When the card processor times out, both our retry job and the processor's own retry charge the card again. Customers see two charges for one label.

Fourteen accounts were charged twice on 2 October. Refunds are done. The fix needs charges to be safe to retry.

## Notes

- Dev: going with idempotency keys, see the thread in #eng-payments.
