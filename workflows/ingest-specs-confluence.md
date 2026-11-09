---
title: Ingest specs from Confluence
description: Write or update one Spec record per spec page in Confluence.
icon: file-lines
on:
  connector: atlassian
  trigger: searchConfluenceUsingCql
  with:
    cloudId: acme.atlassian.net
    cql: type = page AND label = spec ORDER BY lastmodified DESC
    limit: 50
files:
  '**': read-only
  specs: read-write
  log.md: read-write
---

You keep Spec records in step with spec pages in Confluence, one file per page.

The trigger payload is the latest result of `searchConfluenceUsingCql`, most recently modified first. For each page in it that changed since its record was written:

1. Fetch the page with the Confluence tools: title, labels, author, last edit time and body.
2. Write `specs/confluence-<page-id>.md`, like `specs/confluence-884213.md`. If the file exists, update it in place.
3. Set the frontmatter from `types/Spec.md`:
   - `type: Spec`, `title`, `resource` (its Confluence URL)
   - `kind`: `prd`, `rfc` or `tdd`, from a label of the same name or the title
   - `state`: `approved` if it has the `approved` label, `in review` if it has `in-review`, otherwise `draft`
   - `author`, `approved_at` when it's approved
   - `systems`: always set it, one `/systems/<name>.md` per `system-<name>` label, or the page in `systems/` with that title. With no such label, use the page's space name in kebab case. The pages may not exist yet: Update systems creates them as drafts.
4. Write the body as the page content converted to Markdown. Keep the author's headings and wording.

Never edit records in other folders.

Finally, add one line to `log.md` under today's `## YYYY-MM-DD` heading (create it at the top if missing):
`- **Ingest** <n> Confluence specs into specs/, by ingest-specs-confluence.`
