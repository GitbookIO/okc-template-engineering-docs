---
type: Discussion
title: Fixing out-of-order webhooks
resource: 'mock://discussions/2'
channel: eng-platform
participants: ['Tomás Silva', Jonah Park, Priya Raman]
date: 2026-10-28
---

> **Jonah Park:** ENG-226 is the worker pool. Options: partition the queue by shipment ID, add sequence numbers and let customers reorder, or go back to one consumer.
>
> **Tomás Silva:** Sequence numbers push the work onto every customer. One consumer brings the 14 October backlog back.
>
> **Priya Raman:** The dashboard log would also be easier with per-shipment order.
>
> **Tomás Silva:** Partition by shipment ID then. Parallel across shipments, ordered within one. Jonah, can you take it?
>
> **Jonah Park:** On it.
