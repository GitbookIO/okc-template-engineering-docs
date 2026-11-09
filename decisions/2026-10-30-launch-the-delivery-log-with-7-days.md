---
type: Decision
title: Launch the delivery log with 7 days
description: "The dashboard delivery log launches with 7 days of attempts and a status filter, and goes to 30 days later."
state: accepted
decided_on: 2026-10-30
deciders: [Priya Raman, Sofia Lund, Jonah Park]
systems: [/systems/customer-dashboard.md]
sources:
  - id: discussions-mock-6
    resource: /discussions/mock-6.md
    title: "Delivery log scope for launch"
generated:
  by: workflow:record-decisions:anthropic/claude-opus-5-5
  at: 2026-10-30T15:00:00Z
stale_after: 2027-04-28T15:00:00Z
---

## Decision

The delivery log launches with 7 days of attempts and a status filter. It goes to 30 days, with an event type filter, after webhook delivery is partitioned.[^discussions-mock-6]

## Options considered

```mermaid
flowchart TD
  q["What does the delivery log launch with?"]
  q --> o0["7 days, status filter"]
  q --> o1["30 days, both filters"]
  classDef chosen fill:#d3f9d8,stroke:#2b8a3e
  class o0 chosen
```

- **7 days, status filter** (chosen): the query takes under a second.
- **30 days, both filters**: the query takes 9 seconds for big accounts.

## Reasons

- Querying 30 days takes 9 seconds for big accounts, 7 days under one.[^discussions-mock-6]
- Partitioning lets attempts be indexed by shipment, which should make 30 days fast.[^discussions-mock-6]

## Consequences

- The dashboard falls short of the delivery log PRD until the follow-up ships. See [Show a webhook delivery log in the dashboard](2026-10-20-webhook-delivery-log-in-the-dashboard.md).

## Who decided

Priya Raman, Sofia Lund and Jonah Park, on 30 October 2026.
