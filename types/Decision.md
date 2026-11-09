---
type: Type
title: Decision
description: A choice that was made, with its reasons and who made it.
schema:
  type: object
  properties:
    state:
      type: string
      enum: [proposed, accepted, superseded]
      description: Whether it still holds.
    decided_on:
      type: string
      format: date
      description: Day it was decided.
    deciders:
      type: array
      description: People who made the call.
      items:
        type: string
    systems:
      type: array
      description: Systems it affects.
      items:
        type: string
        pattern: '^/systems/[^/]+\.md$'
    supersedes:
      type: string
      pattern: '^/decisions/[^/]+\.md$'
      description: Earlier decision it replaces.
---

A Decision page records what was decided, the options, the reasons and who decided, so the reasons outlive the meeting or thread they came from.

- **Layer:** concept. Written by refinement workflows, which cite the records they read in `sources` and set `generated`. People review every change on its branch.
- **Folder:** `decisions/`
- **Filenames:** `decisions/<date>-<slug>.md`, like `decisions/2026-10-30-move-retries-to-queue.md`.
- **Refined from:** Meetings, discussions and specs.

Example frontmatter:

```yaml
type: Decision
title: Move charge retries to the job queue
state: accepted
decided_on: 2026-10-30
deciders: [Lena Ito, Dev Okafor]
```
