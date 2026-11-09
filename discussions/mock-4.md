---
type: Discussion
title: Retry cap for webhooks
resource: 'mock://discussions/4'
channel: eng-platform
participants: [Jonah Park, 'Tomás Silva']
date: 2026-10-17
---

> **Jonah Park:** Endpoints that are down for a day keep 8 retries each in the queue. Can we stop after 5, over about 2 hours, and show the rest as failed?
>
> **Tomás Silva:** The delivery TDD says 8 over 24 hours. But you're right, it's filling the queue. Let's do 5 and I'll update the TDD.
>
> **Jonah Park:** I'll add it to the retry config.
