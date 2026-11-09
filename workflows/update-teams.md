---
title: Update teams
description: Keep each Team page current from the System pages it owns.
icon: users
on: systems/**
commit: branch
files:
  '**': read-only
  teams: read-write
  log.md: read-write
---

You keep Team pages in `teams/` current from the System pages. This runs after an Update systems branch merges, so you read reviewed System pages, not raw records.

1. Read the System pages that changed. Collect the teams they name in `team`.
2. For each of those teams, read every System page whose `team` is that team, and the current `teams/<slug>.md`. If a team has no page yet, create `teams/<slug>.md` for it, using the slug from the link, with `status: draft`, a `title` from the slug and a one-line `description` of what it owns. Leave out `lead` and `channel` until a person adds them. People remove `status: draft` once they've reviewed the page, so never add it to an existing page or remove it yourself.
3. Frontmatter from `types/Team.md`: keep `type`, `title`, `description`, `lead` and `channel`. Set `systems` to every system the team owns, sorted by title. Set `sources` to those System pages (with `resource` as the bundle path and `id` as `systems-<slug>`), `generated` to the workflow signature you were given with `at` now, and `stale_after` to 30 days later.
4. Body:
   - One paragraph on what the team owns and what it's working on now.
   - `## Systems`: one line per system with its lifecycle and a footnote.
   - `## What's changing`: the most important recent changes across its systems, from their Recent changes sections, at most five, with footnotes.
   - `## Needs attention`: drift findings and open incidents from its System pages, with footnotes. Write `Nothing right now.` if there are none.

Don't write about individual people beyond the lead. Keep what people wrote by hand.

Keep `teams/index.md` as a list of every team: `- [<title>](<slug>.md): <description>`, sorted by title.

Finally, add one line to `log.md` under today's `## YYYY-MM-DD` heading (create it at the top if missing):
`- **Update** <team titles> from <n> System pages, by update-teams.`
