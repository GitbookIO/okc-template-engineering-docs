---
type: Type
title: Pull Request
description: A code change from a Git host, one file per pull request.
schema:
  type: object
  properties:
    number:
      type: integer
      description: Pull request number in its repository.
      minimum: 0
    repository:
      type: string
      description: Repository, as owner/name.
    state:
      type: string
      enum: [open, merged, closed]
      description: Open, merged, or closed without merging.
    author:
      type: string
      description: Name or handle of the author.
    merged_at:
      type: string
      format: date-time
      description: When it was merged.
    issues:
      type: array
      description: Issues it fixes or refers to.
      items:
        type: string
        pattern: '^/issues/[^/]+\.md$'
    systems:
      type: array
      description: Systems it changes.
      items:
        type: string
        pattern: '^/systems/[^/]+\.md$'
  required: [state]
---

A pull request records a change to code: what changed, why, and which issues and systems it touches. Its body keeps the description the author wrote, since that is where intent lives.

- **Layer:** record. Written by ingest workflows, one file per source event. Refinements read records and never edit them.
- **Folder:** `prs/`
- **Filenames:** `prs/<source>-<repository>-<number>.md`, like `prs/github-acme-billing-412.md`. Mocks are `prs/mock-<n>.md` with `resource: mock://prs/<n>`.
- **Ingested from:** GitHub, GitLab, Bitbucket, Azure Repos, or local changes under `packages/**` in a docs-in-code repo.

Example frontmatter:

```yaml
type: Pull Request
title: Make charge retries idempotent
resource: mock://prs/9
state: merged
author: dev.okafor
merged_at: 2026-11-04T15:20:00Z
issues: [/issues/mock-14.md]
systems: [/systems/billing-api.md]
```
