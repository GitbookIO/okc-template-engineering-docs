---
type: Type
title: Runbook
description: Steps for handling a known kind of problem.
schema:
  type: object
  properties:
    system:
      type: string
      pattern: '^/systems/[^/]+\.md$'
      description: System it is for.
    team:
      type: string
      pattern: '^/teams/[^/]+\.md$'
      description: Team that runs it.
---

A Runbook says how to recognize a problem and what to do, step by step, learned from past incidents and the fixes that followed them.

- **Layer:** concept. Written by refinement workflows, which cite the records they read in `sources` and set `generated`. People review every change on its branch.
- **Folder:** `runbooks/`
- **Filenames:** `runbooks/<slug>.md`, like `runbooks/card-processor-timeouts.md`.
- **Refined from:** Incidents and pull requests.

Example frontmatter:

```yaml
type: Runbook
title: Card processor timeouts
system: /systems/billing-api.md
team: /teams/payments.md
```
