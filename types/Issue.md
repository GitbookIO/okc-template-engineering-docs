---
type: Type
title: Issue
description: A work item from an issue tracker, one file per issue.
schema:
  type: object
  properties:
    identifier:
      type: string
      description: Key in the source tool, like ENG-123.
    state:
      type: string
      description: Workflow state as the source tool names it, like backlog, in progress, done or canceled.
    priority:
      type: string
      enum: [urgent, high, medium, low, none]
      description: Priority, mapped onto one shared scale.
    assignee:
      type: string
      description: Name or handle of the person it is assigned to.
    labels:
      type: array
      description: Labels from the source tool.
      items:
        type: string
    system:
      type: string
      pattern: '^/systems/[^/]+\.md$'
      description: System the issue is about.
    team:
      type: string
      pattern: '^/teams/[^/]+\.md$'
      description: Team that owns the issue.
    project:
      type: string
      pattern: '^/projects/[^/]+\.md$'
      description: Project the issue belongs to.
    account:
      type: string
      pattern: '^/accounts/[^/]+\.md$'
      description: Customer account that raised or is affected by the issue.
    created_at:
      type: string
      format: date-time
      description: When the issue was created.
    updated_at:
      type: string
      format: date-time
      description: When the issue last changed.
    closed_at:
      type: string
      format: date-time
      description: When the issue was closed, if it is.
  required: [state]
---

An issue is a unit of planned or reported work: a bug, a task, a feature request. Linear, Jira and GitHub Issues all land in this one type. Fields only one tool has go in extra frontmatter keys.

- **Layer:** record. Written by ingest workflows, one file per source event. Refinements read records and never edit them.
- **Folder:** `issues/`
- **Filenames:** `issues/<source>-<key>.md`, like `issues/linear-ENG-123.md` or `issues/jira-PLAT-88.md`. Mocks are `issues/mock-<n>.md` with `resource: mock://issues/<n>`.
- **Ingested from:** Linear, Jira, GitHub Issues, GitLab Issues, Asana, Shortcut, ClickUp, Azure Boards.

Example frontmatter:

```yaml
type: Issue
title: Payment retries fire twice after a timeout
resource: mock://issues/14
identifier: ENG-214
state: in progress
priority: high
system: /systems/billing-api.md
team: /teams/payments.md
```
