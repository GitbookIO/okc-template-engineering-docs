# Workflows

Each Markdown file in this folder is a workflow, except this README. Its frontmatter says when it runs and what it may touch, and its body is the prompt the agent follows.

There are two layers:

- **Ingest workflows** (`ingest-*.md`) turn source events into records, one file per event. They read a connection or `inbox/`, write only record folders and `log.md`, and commit to the branch that triggered them.
- **Refinement workflows** read across records and keep the concept pages current. They write only concept folders and `log.md`, watch `main`, and put every change on its own branch for review. Comment on that branch and the same workflow revises its work.

Every run appends one line to `log.md`.

| Workflow | Layer | Trigger | Writes |
| --- | --- | --- | --- |
| [Ingest pull requests from GitHub](ingest-prs-github.md) | Ingest | `github`, polls `search_pull_requests` | `prs/` |
| [Ingest issues from Linear](ingest-issues-linear.md) | Ingest | `linear`, polls `list_issues` | `issues/` |
| [Ingest issues from Jira](ingest-issues-jira.md) | Ingest | `atlassian`, polls `searchJiraIssuesUsingJql` | `issues/` |
| [Ingest incidents from Sentry](ingest-incidents-sentry.md) | Ingest | `sentry`, polls `search_issues` for resolved issues | `incidents/` |
| [Ingest specs from Notion](ingest-specs-notion.md) | Ingest | `notion`, polls `notion-query-data-sources` | `specs/` |
| [Ingest specs from Confluence](ingest-specs-confluence.md) | Ingest | `atlassian`, polls `searchConfluenceUsingCql` | `specs/` |
| [Ingest inbox](ingest-inbox.md) | Ingest | `inbox/**`, any branch | `prs/`, `incidents/`, `specs/` or `discussions/`, then moves the original to `archive/` |
| [Update systems](update-systems.md) | Refinement | `prs/`, `issues/`, `incidents/` or `specs/` change on `main` | `systems/`, including drift from approved specs, and drafts for new systems |
| [Update runbooks](update-runbooks.md) | Refinement | `incidents/` change on `main` | `runbooks/` |
| [Record decisions](record-decisions.md) | Refinement | `discussions/` or `specs/` change on `main` | `decisions/` |
| [Update teams](update-teams.md) | Refinement | `systems/` change on `main` | `teams/`, and drafts for new teams |
| [System skills](system-skills.md) | Refinement | Mondays at 07:00 | `skills/` |
| [Weekly digest](weekly-digest.md) | Refinement | Mondays at 08:00 | `digests/` |

Update teams reads System pages, so it runs after an Update systems branch merges. That puts a review between the two layers.
