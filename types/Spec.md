---
type: Type
title: Spec
description: A product or technical spec, one file per document.
schema:
  type: object
  properties:
    kind:
      type: string
      enum: [prd, rfc, tdd]
      description: Product requirements, request for comments, or technical design.
    state:
      type: string
      enum: [draft, in review, approved]
      description: Where the spec is in review.
    author:
      type: string
      description: Name or handle of the author.
    systems:
      type: array
      description: Systems the spec covers.
      items:
        type: string
        pattern: '^/systems/[^/]+\.md$'
    approved_at:
      type: string
      format: date-time
      description: When it was approved.
  required: [kind, state]
---

A spec says how something should work. It is a record even when someone writes it directly in this repo, which works like a manual ingest. Refinements never edit specs. They compare them with what shipped and put drift findings on System pages.

- **Layer:** record. Written by ingest workflows, one file per source event. Refinements read records and never edit them.
- **Folder:** `specs/`
- **Filenames:** `specs/<source>-<id>.md`, like `specs/notion-3f9a.md`, or a kebab-case title for specs written here. Mocks are `specs/mock-<n>.md` with `resource: mock://specs/<n>`.
- **Ingested from:** Notion, Confluence, Google Docs, Coda, or written in this repo.

Example frontmatter:

```yaml
type: Spec
title: Idempotent charges
resource: mock://specs/2
kind: rfc
state: approved
author: lena.ito
systems: [/systems/billing-api.md]
```
