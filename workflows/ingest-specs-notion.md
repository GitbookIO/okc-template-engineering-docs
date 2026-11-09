---
title: Ingest specs from Notion
description: Write or update one Spec record per page in the Notion specs database.
icon: file-lines
on:
  connector: notion
  trigger: notion-query-data-sources
  with:
    mode: rows
    data_source_url: collection://acme-specs
    sort:
      - timestamp: last_edited_time
        direction: descending
    limit: 50
files:
  '**': read-only
  specs: read-write
  log.md: read-write
---

You keep Spec records in step with the specs database in Notion, one file per page.

The trigger payload is the latest rows of the specs database, most recently edited first. For each page in it that changed since its record was written:

1. Fetch the page with the Notion tools: title, properties, author, last edit time and full content.
2. Write `specs/notion-<page-id>.md`, using the first 8 characters of the page ID, like `specs/notion-3f9a12bc.md`. If the file exists, update it in place.
3. Set the frontmatter from `types/Spec.md`:
   - `type: Spec`, `title`, `resource` (its Notion URL)
   - `kind`: `prd`, `rfc` or `tdd`, from the page's Type property or its title
   - `state`: `draft`, `in review` or `approved`, from the page's Status property. If it has none, use `draft`.
   - `author`, `approved_at` when it's approved
   - `systems`: always set it, from the page's Systems property, one `/systems/<name in kebab case>.md` per value, or the page in `systems/` with that title. The pages may not exist yet: Update systems creates them as drafts.
4. Write the body as the page content converted to Markdown. Keep the author's headings and wording.

Never edit records in other folders.

Finally, add one line to `log.md` under today's `## YYYY-MM-DD` heading (create it at the top if missing):
`- **Ingest** <n> Notion specs into specs/, by ingest-specs-notion.`
