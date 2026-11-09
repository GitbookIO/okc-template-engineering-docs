---
type: Discussion
title: Rate cache TTL
resource: 'mock://discussions/3'
channel: eng-shipping
participants: [Lena Ito, Ravi Menon, Ana Kovac]
date: 2026-10-27
---

> **Lena Ito:** Carrier rate calls are our second largest infra cost. If we keep rates for 60 minutes instead of 15, calls drop by about 70 percent.
>
> **Ana Kovac:** The quotes PRD says 15 minutes. Is an hour safe?
>
> **Ravi Menon:** Price-change notices still clear the cache, so we never quote a rate after a change. The risk is small rate updates carriers don't announce.
>
> **Lena Ito:** Let's go to 60 minutes and watch quote accuracy for two weeks.
>
> **Ana Kovac:** Fine with me. I'll update the PRD after we see the numbers.
