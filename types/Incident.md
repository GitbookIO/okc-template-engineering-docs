---
type: Type
title: Incident
description: A production problem from an error tracker or paging tool, one file per incident.
schema:
  type: object
  properties:
    severity:
      type: string
      enum: [critical, high, medium, low]
      description: Severity, mapped onto one shared scale.
    state:
      type: string
      enum: [open, resolved]
      description: Whether the incident is still going on.
    system:
      type: string
      pattern: '^/systems/[^/]+\.md$'
      description: System where it happened.
    started_at:
      type: string
      format: date-time
      description: When it started.
    resolved_at:
      type: string
      format: date-time
      description: When it was resolved.
    issues:
      type: array
      description: Follow-up issues.
      items:
        type: string
        pattern: '^/issues/[^/]+\.md$'
  required: [severity, started_at]
---

An incident records something that went wrong in production: what people saw, the timeline, and how it was fixed. Runbooks and System pages are refined from these.

- **Layer:** record. Written by ingest workflows, one file per source event. Refinements read records and never edit them.
- **Folder:** `incidents/`
- **Filenames:** `incidents/<source>-<id>.md`, like `incidents/sentry-4821.md`. Mocks are `incidents/mock-<n>.md` with `resource: mock://incidents/<n>`.
- **Ingested from:** Sentry, PagerDuty, incident.io, Opsgenie, Datadog.

Example frontmatter:

```yaml
type: Incident
title: Checkout errors after the card processor timed out
resource: mock://incidents/3
severity: high
state: resolved
system: /systems/billing-api.md
started_at: 2026-10-28T09:12:00Z
resolved_at: 2026-10-28T10:05:00Z
```
