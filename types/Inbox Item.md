---
type: Type
title: Inbox Item
description: Something dropped into the inbox for an ingest workflow to sort.
schema:
  type: object
  properties: {}
---

The inbox takes pasted text and files without any connection set up. Ingest inbox reads each new item, writes the records it describes, and moves the original to `archive/`. Most items are untyped. The typed example file stays so the workflow graph shows the inbox.

- **Layer:** record. Written by ingest workflows, one file per source event. Refinements read records and never edit them.
- **Folder:** `inbox/`
- **Filenames:** Anything. Ingest inbox never moves `inbox/example.md`.
- **Ingested from:** People pasting or uploading, and agents connected over MCP.

Example frontmatter:

```yaml
type: Inbox Item
title: Example inbox item
```
