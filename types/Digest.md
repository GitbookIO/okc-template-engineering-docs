---
type: Type
title: Digest
description: A summary of what changed over a period.
schema:
  type: object
  properties:
    period_start:
      type: string
      format: date
      description: First day covered.
    period_end:
      type: string
      format: date
      description: Last day covered.
  required: [period_start, period_end]
---

A Digest says what happened over a week: what landed, what changed and what needs attention, counted from `log.md` and the records of that week.

- **Layer:** concept. Written by refinement workflows, which cite the records they read in `sources` and set `generated`. People review every change on its branch.
- **Folder:** `digests/`
- **Filenames:** `digests/<period_end>.md`, like `digests/2026-11-08.md`.
- **Refined from:** `log.md` and the period's records.

Example frontmatter:

```yaml
type: Digest
title: Week of 2 November 2026
period_start: 2026-11-02
period_end: 2026-11-08
```
