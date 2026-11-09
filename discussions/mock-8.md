---
type: Discussion
title: Carrier timeouts
resource: 'mock://discussions/8'
channel: incident-labels
participants: [Lena Ito, Ravi Menon, Jonah Park]
date: 2026-10-24
---

> **Ravi Menon:** Label calls have no timeout, which is why every worker is stuck.
>
> **Jonah Park:** What does the carrier usually take? Our p99 is about 3 seconds.
>
> **Lena Ito:** Then time out at 8 seconds and return a retryable error. A circuit breaker after that, but the timeout ships today.
>
> **Ravi Menon:** Agreed, I'll open the PR.
