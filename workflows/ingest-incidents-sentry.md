---
title: Ingest incidents from Sentry
description: Write one Incident record per resolved Sentry issue.
icon: siren
on:
  connector: sentry
  trigger: search_issues
  with:
    organizationSlug: acme
    query: is:resolved
    sort: new
files:
  '**': read-only
  incidents: read-write
  log.md: read-write
---

You turn resolved Sentry issues into Incident records, one file per incident.

The trigger payload is the latest result of `search_issues` for `is:resolved`, newest first. For each issue in it that has no record yet:

1. Fetch its details with the Sentry tools: title, first and last seen, resolution time, event count, users affected, project, culprit and the latest event's stack trace.
2. Write `incidents/sentry-<short-id>.md`, like `incidents/sentry-SHIP-4F2.md`. If the file exists, update it in place.
3. Set the frontmatter from `types/Incident.md`:
   - `type: Incident`, `title`, `resource` (its Sentry URL)
   - `severity`: `critical` if it took a service down or affected payments, `high` if more than 100 users saw it, `medium` if fewer, `low` otherwise
   - `state: resolved`, `started_at` (first seen), `resolved_at`
   - `system`: always `/systems/<Sentry project slug>.md`, or the page in `systems/` whose `repository` or title matches the project. The page may not exist yet: Update systems creates it as a draft.
   - `issues`: bundle paths of Issue records linked from the Sentry issue, matched by `identifier`.
4. Write the body with `## What happened` (two or three sentences on what people saw), `## Timeline` (first seen, peak, resolution) and `## Cause`, using only what Sentry shows. Write "Unknown" rather than guess.

Never edit records in other folders.

Finally, add one line to `log.md` under today's `## YYYY-MM-DD` heading (create it at the top if missing):
`- **Ingest** <n> resolved Sentry issues into incidents/, by ingest-incidents-sentry.`
