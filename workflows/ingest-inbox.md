---
title: Ingest inbox
description: Sort what people drop into the inbox into records, and archive the originals.
icon: inbox
on:
  path: inbox/**
  branches: ['main', '*']
files:
  '**': read-only
  '{prs,incidents,specs,discussions}/**': read-write
  inbox: read-write
  archive: read-write
  log.md: read-write
---

You sort new files in `inbox/` into records. People drop pasted pull request descriptions, incident notes, specs and chat threads here when no connection brings them in.

For each new or changed file in `inbox/` that triggered this run, except `inbox/example.md`, which you never touch:

1. Read it and decide what it is:
   - a pull request description or a merged change: a Pull Request, in `prs/`
   - notes about something that broke in production: an Incident, in `incidents/`
   - a PRD, RFC or design document: a Spec, in `specs/`
   - a chat thread or a back-and-forth between people: a Discussion, in `discussions/`
   If it holds several, write one record each. If it's none of these, leave it in `inbox/` and say so in the log line.
2. Read `systems/`, `teams/` and the existing records first. Always set `system` or `systems`: use the page whose title or `repository` the text names, or, if the text names a repository or system with no page yet, `/systems/<its name in kebab case>.md`. Update systems creates missing pages as drafts. Link issues only by keys that have a record, and never invent a person.
3. Write each record as `<folder>/inbox-<YYYY-MM-DD>-<slug>.md`, like `prs/inbox-2026-11-09-retry-backoff.md`, with the frontmatter its type in `types/` describes. Set `resource` to the bundle path the original will have in `archive/`. Use today's date for any time the text doesn't give, with an offset.
4. Keep the original wording in the body. Add only what's needed to make it a record: a title, and the links in frontmatter.
5. Move the original to `archive/<YYYY-MM-DD>-<original filename>`.

Never edit concept pages or existing records.

Finally, add one line to `log.md` under today's `## YYYY-MM-DD` heading (create it at the top if missing):
`- **Ingest** <what was dropped> into <folders>, by ingest-inbox.`
