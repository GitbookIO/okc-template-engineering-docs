---
type: Type
title: System
description: A service, app or component, with what is known about it now.
schema:
  type: object
  properties:
    team:
      type: string
      pattern: '^/teams/[^/]+\.md$'
      description: Team that owns it.
    lifecycle:
      type: string
      enum: [experimental, production, deprecated]
      description: Where it is in its life.
    depends_on:
      type: array
      description: Systems it calls or needs.
      items:
        type: string
        pattern: '^/systems/[^/]+\.md$'
    specs:
      type: array
      description: Specs that describe it.
      items:
        type: string
        pattern: '^/specs/[^/]+\.md$'
    runbooks:
      type: array
      description: Runbooks for it.
      items:
        type: string
        pattern: '^/runbooks/[^/]+\.md$'
    repository:
      type: string
      description: Code repository, as owner/name.
---

A System page says what a system does, who owns it, what it depends on, what changed recently and where it drifts from its approved specs.

- **Layer:** concept. Written by refinement workflows, which cite the records they read in `sources` and set `generated`. People review every change on its branch.
- **Folder:** `systems/`
- **Filenames:** `systems/<slug>.md`, like `systems/billing-api.md`.
- **Refined from:** Pull requests, issues, incidents, specs and decisions.

Example frontmatter:

```yaml
type: System
title: Billing API
team: /teams/payments.md
lifecycle: production
depends_on: [/systems/ledger.md]
```
