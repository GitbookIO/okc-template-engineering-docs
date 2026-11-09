---
title: Ingest issues from Linear
description: Write or update one Issue record per Linear issue.
icon: list-check
on:
  connector: linear
  trigger: list_issues
  with:
    orderBy: updatedAt
    limit: 50
files:
  '**': read-only
  issues: read-write
  log.md: read-write
---

You keep Issue records in step with Linear, one file per issue.

The trigger payload is the latest result of `list_issues`, most recently updated first. For each issue in it that changed since its record was written:

1. Fetch the issue with the Linear tools if the payload lacks its description, state, priority, assignee, labels or team.
2. Write `issues/linear-<identifier>.md`, like `issues/linear-ENG-214.md`. If the file exists, update it in place.
3. Set the frontmatter from `types/Issue.md`:
   - `type: Issue`, `title`, `resource` (its Linear URL), `identifier`
   - `state`: the Linear workflow state, lowercased, like `backlog`, `in progress`, `done` or `canceled`
   - `priority`: Linear's Urgent, High, Medium, Low and No priority become `urgent`, `high`, `medium`, `low` and `none`
   - `assignee`, `labels`, `created_at`, `updated_at`, and `closed_at` when it's done or canceled
   - `system`: always set it. Use the issue's `system:<name>` label if it has one, like `system:billing-api` for `/systems/billing-api.md`. Otherwise use the Linear team name in kebab case. If a page in `systems/` has that title under another slug, use that page. The page may not exist yet: Update systems creates it as a draft.
   - `team`: always `/teams/<Linear team name in kebab case>.md`, or the page in `teams/` with that title. It may not exist yet: Update teams creates it.
4. Write the body as the issue description. Add new comments that carry decisions or findings under `## Notes`, newest last.

Never edit records in other folders.

Finally, add one line to `log.md` under today's `## YYYY-MM-DD` heading (create it at the top if missing):
`- **Ingest** <n> Linear issues into issues/, by ingest-issues-linear.`
