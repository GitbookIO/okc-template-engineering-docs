---
title: Weekly digest
description: Summarize last week's changes, incidents, decisions and drift.
icon: newspaper
on:
  event: schedule
  schedule: 0 8 * * 1
commit: branch
files:
  '**': read-only
  digests: read-write
  log.md: read-write
---

Every Monday, you write one digest of the week that just ended, Monday to Sunday.

1. Read `log.md` for that week, then the records dated in it: pull requests by `merged_at`, issues by `created_at` and `closed_at`, incidents by `started_at`, specs by `approved_at`, and discussions by `date`. Read the decisions dated in it, and the Drift from spec sections of the System pages.
2. Write `digests/<YYYY-MM-DD>.md`, named after the Sunday the week ends on.
3. Frontmatter from `types/Digest.md`: `type: Digest`, `title` ("Week of <D Month YYYY>", the Monday), `description` (the week in one line), `period_start`, `period_end`, `sources` (every record and page cited, with `resource` as the bundle path and `id` as `<folder>-<filename without .md>`) and `generated` (the workflow signature you were given, `at` now).
4. Body:
   - One paragraph: the most important thing that happened, with counts of pull requests merged, issues opened and closed, and incidents.
   - A Vega-Lite bar chart in a `vega-lite` code block of pull requests merged per system that week.
   - `## Shipped`: merged pull requests grouped by system, one line each with a footnote.
   - `## Incidents`: each incident, its severity and how long it lasted, with a footnote.
   - `## Decisions`: decisions dated that week, with footnotes.
   - `## Drift from spec`: open drift findings from the System pages, with footnotes.
   - `## Needs attention`: urgent or high-priority issues still open, with footnotes.

Count only what the records show. Leave a section out if it would be empty.

Keep `digests/index.md` as a list of every digest, newest first: `- [<title>](<file>.md): <description>`.

Finally, add one line to `log.md` under today's `## YYYY-MM-DD` heading (create it at the top if missing):
`- **Write** the digest for the week of <date>, by weekly-digest.`
