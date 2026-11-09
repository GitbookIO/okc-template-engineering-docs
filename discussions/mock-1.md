---
type: Discussion
title: 'How do we stop double charges?'
resource: 'mock://discussions/1'
channel: eng-payments
participants: [Maya Chen, Dev Okafor, Ana Kovac]
date: 2026-10-12
---

> **Maya Chen:** We need charges to be safe to retry. Three options I see: idempotency keys on every charge, asking the processor to dedupe on their side, or a lock per label purchase on our side.
>
> **Dev Okafor:** The processor supports idempotency keys already. Their dedupe needs a contract change. A lock doesn't help when their retry and ours race.
>
> **Ana Kovac:** Keys sound simplest. Does the ledger need the key too?
>
> **Maya Chen:** Yes, so the ledger refuses a second entry even if billing slips. Agreed then: idempotency keys on charges and in the ledger. I'll write the RFC.
>
> **Dev Okafor:** 👍
