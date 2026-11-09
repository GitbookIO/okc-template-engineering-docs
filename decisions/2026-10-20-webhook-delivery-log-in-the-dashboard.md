---
type: Decision
title: Show a webhook delivery log in the dashboard
description: "Customers see 30 days of delivery attempts, filter them, and resend failed events."
state: accepted
decided_on: 2026-10-20
deciders: [Priya Raman]
systems: [/systems/customer-dashboard.md]
sources:
  - id: specs-mock-5
    resource: /specs/mock-5.md
    title: "Webhook delivery log in the dashboard"
generated:
  by: workflow:record-decisions:anthropic/claude-opus-5-5
  at: 2026-10-20T10:00:00Z
stale_after: 2027-04-18T10:00:00Z
---

## Decision

The dashboard shows every delivery attempt from the last 30 days, filters them by status and event type, and resends a failed event with one click.[^specs-mock-5]

## Options considered

```mermaid
flowchart TD
  q["How do customers debug their webhook endpoints?"]
  q --> o0["A delivery log in the dashboard"]
  classDef chosen fill:#d3f9d8,stroke:#2b8a3e
  class o0 chosen
```

- **A delivery log in the dashboard** (chosen): 30 days of attempts, filters by status and event type, one-click resend. The PRD names no other option.

## Reasons

- Customers should fix their own endpoints without writing to support.[^specs-mock-5]

## Consequences

- A later decision launched it with 7 days and a status filter first. See [Launch the delivery log with 7 days](2026-10-30-launch-the-delivery-log-with-7-days.md).

## Who decided

Priya Raman, on 20 October 2026.
