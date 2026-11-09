---
type: Discussion
title: Delivery log scope for launch
resource: 'mock://discussions/6'
channel: eng-web
participants: [Priya Raman, Sofia Lund, Jonah Park]
date: 2026-10-30
---

> **Sofia Lund:** Querying 30 days of delivery attempts takes 9 seconds for big accounts. 7 days takes under one.
>
> **Jonah Park:** Once the queue is partitioned we can index attempts by shipment, which should make 30 days fast.
>
> **Priya Raman:** Then let's launch with 7 days and a status filter, and go to 30 days after the partitioning work. The event type filter can wait too.
