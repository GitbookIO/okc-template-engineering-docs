---
type: Type
title: Team
description: A group of people at Acme and what they own.
schema:
  type: object
  properties:
    lead:
      type: string
      description: Name of the team lead.
    channel:
      type: string
      description: Chat channel to reach the team.
    systems:
      type: array
      description: Systems the team owns.
      items:
        type: string
        pattern: '^/systems/[^/]+\.md$'
---

A Team page says what a team owns and works on. It stops at the team, so there are no pages about individual colleagues.

- **Layer:** concept. Written by refinement workflows, which cite the records they read in `sources` and set `generated`. People review every change on its branch.
- **Folder:** `teams/`
- **Filenames:** `teams/<slug>.md`, like `teams/payments.md`.
- **Refined from:** Systems and projects.

Example frontmatter:

```yaml
type: Team
title: Payments
lead: Lena Ito
channel: '#team-payments'
```
