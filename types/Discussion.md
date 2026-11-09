---
type: Type
title: Discussion
description: A chat thread, one file per thread.
schema:
  type: object
  properties:
    channel:
      type: string
      description: Channel the thread was in.
    participants:
      type: array
      description: Names of the people who took part.
      items:
        type: string
    date:
      type: string
      format: date
      description: Day the thread started.
  required: [channel, date]
---

A discussion keeps one chat thread, since that is often where the reasons behind a decision live. Decisions are refined from these.

- **Layer:** record. Written by ingest workflows, one file per source event. Refinements read records and never edit them.
- **Folder:** `discussions/`
- **Filenames:** `discussions/<source>-<id>.md`, like `discussions/slack-C04-1730.md`. Mocks are `discussions/mock-<n>.md` with `resource: mock://discussions/<n>`.
- **Ingested from:** Slack, Microsoft Teams, Discord.

Example frontmatter:

```yaml
type: Discussion
title: Should retries move to the queue?
resource: mock://discussions/2
channel: eng-billing
participants: [Dev Okafor, Lena Ito]
date: 2026-10-30
```
