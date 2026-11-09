---
title: Ingest issues from Jira
description: Write or update one Issue record per Jira issue.
icon: list-check
on:
  connector: atlassian
  trigger: searchJiraIssuesUsingJql
  with:
    cloudId: acme.atlassian.net
    jql: project = ENG ORDER BY updated DESC
    maxResults: 50
files:
  '**': read-only
  issues: read-write
  log.md: read-write
---

You keep Issue records in step with Jira, one file per issue.

The trigger payload is the latest result of `searchJiraIssuesUsingJql`, most recently updated first. For each issue in it that changed since its record was written:

1. Fetch the issue with the Jira tools if the payload lacks its description, status, priority, assignee, labels, components or team.
2. Write `issues/jira-<key>.md`, like `issues/jira-ENG-88.md`. If the file exists, update it in place.
3. Set the frontmatter from `types/Issue.md`:
   - `type: Issue`, `title`, `resource` (its Jira URL), `identifier` (the key)
   - `state`: the Jira status, lowercased, like `to do`, `in progress` or `done`
   - `priority`: Jira's Highest, High, Medium, Low and Lowest become `urgent`, `high`, `medium`, `low` and `none`
   - `assignee`, `labels`, `created_at`, `updated_at`, and `closed_at` when it's resolved
   - `system`: always set it, from the issue's first component in kebab case, like `/systems/billing-api.md`. With no component, use the project name. If a page in `systems/` has that title under another slug, use that page. The page may not exist yet: Update systems creates it as a draft.
   - `team`: always `/teams/<team in kebab case>.md`, from the Jira team field, or the project name without one. It may not exist yet: Update teams creates it.
   - Keep Jira-only fields, like `components` or `sprint`, as extra keys.
4. Write the body as the issue description. Add new comments that carry decisions or findings under `## Notes`, newest last.

Never edit records in other folders.

Finally, add one line to `log.md` under today's `## YYYY-MM-DD` heading (create it at the top if missing):
`- **Ingest** <n> Jira issues into issues/, by ingest-issues-jira.`
