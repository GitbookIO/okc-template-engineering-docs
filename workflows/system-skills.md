---
title: System skills
description: Write an agent skill for each busy system, on how to change it safely.
icon: graduation-cap
on:
  event: schedule
  schedule: 0 7 * * 1
commit: branch
files:
  '**': read-only
  skills: read-write
  log.md: read-write
---

Every Monday, you write agent skills in `skills/`: one per busy system, telling Claude or Codex how to change that system safely. Each is a folder with a `SKILL.md` that follows the Agent Skills spec.

1. Count merged pull requests per system over the last 30 days, from `prs/`. A system with 3 or more is busy.
2. For each busy system, read its System page, its approved specs, its runbooks, the decisions that link to it, and its pull requests from the last 30 days.
3. Write `skills/<system-slug>/SKILL.md`, like `skills/billing-api/SKILL.md`:
   - Frontmatter: `name` (the system slug, matching the folder), `description` ("How to change the <title> safely. Use when working on <the areas its pull requests touched>.", under 1024 characters), `type: Skill`, `system` (its page), `sources` (with `resource` as the bundle path and `id` as `<folder>-<filename without .md>`) and `generated` (the workflow signature you were given, `at` now).
   - `## What it is`: two sentences from the System page.
   - `## Rules from specs`: each requirement of its approved specs that a change could break, one line each with a footnote. Put open drift findings first.
   - `## How changes are made here`: patterns the recent pull requests follow, like where tests go or which flags guard rollouts, with footnotes.
   - `## Before you merge`: checks drawn from its incidents and runbooks.
4. Keep it under 150 lines. Leave skills for systems that aren't busy this week as they are.

Keep `skills/index.md` as a list of every skill: `- [<name>](<name>/SKILL.md): <description>`, sorted by name.

Finally, add one line to `log.md` under today's `## YYYY-MM-DD` heading (create it at the top if missing):
`- **Write** skills for <system titles>, by system-skills.`
