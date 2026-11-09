---
title: Update runbooks
description: Turn resolved incidents into runbooks, one per kind of problem.
icon: book
on: incidents/**
commit: branch
files:
  '**': read-only
  runbooks: read-write
  log.md: read-write
---

You keep runbooks in `runbooks/`: how to recognize a known kind of problem and what to do about it, learned from past incidents.

For each Incident record that triggered this run:

1. Read it, the System page it links to, and every other incident on that system.
2. Find the runbook for this kind of problem: one in `runbooks/` with the same `system` whose "When to use" matches these symptoms. If there isn't one and the incident has a clear cause and fix, create `runbooks/<slug>.md`, where the slug names the problem, like `carrier-api-timeouts`. If the cause is unknown, don't create a runbook.
3. Write the frontmatter from `types/Runbook.md`: `type: Runbook`, `title`, `description` (one line), `system`, `team` (the system page's `team`), `sources` (every incident cited, with `resource` as its bundle path and `id` as `incidents-<filename without .md>`), `generated` (the workflow signature you were given, `at` now) and `stale_after` (30 days later).
4. Write the body:
   - `## When to use`: the symptoms people see, in their words.
   - `## Check`: numbered steps to confirm it's this problem.
   - `## Fix`: numbered steps that fixed it before, citing the incident for each.
   - `## Escalate`: who to tell, from the system's team page, and when.
   - `## Past incidents`: one line per incident, newest first, with a footnote.

Keep steps that people added by hand. Only add what the incidents show.

Keep `runbooks/index.md` as a list of every runbook: `- [<title>](<slug>.md): <description>`, sorted by title.

Finally, add one line to `log.md` under today's `## YYYY-MM-DD` heading (create it at the top if missing):
`- **Update** <runbook titles> from <n> incidents, by update-runbooks.`
