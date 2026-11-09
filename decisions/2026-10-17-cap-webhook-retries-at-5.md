---
type: Decision
title: Cap webhook retries at 5 attempts
description: "Failed deliveries stop after 5 attempts over about 2 hours, instead of 8 over 24 hours."
state: accepted
decided_on: 2026-10-17
deciders: [Jonah Park, Tomás Silva]
systems: [/systems/webhooks.md]
sources:
  - id: discussions-mock-4
    resource: /discussions/mock-4.md
    title: "Retry cap for webhooks"
  - id: specs-mock-2
    resource: /specs/mock-2.md
    title: "Webhook delivery guarantees"
generated:
  by: workflow:record-decisions:anthropic/claude-opus-5-5
  at: 2026-10-17T12:00:00Z
stale_after: 2027-04-15T12:00:00Z
---

## Decision

A failed delivery is retried 5 times over about 2 hours, then shown as failed.[^discussions-mock-4]

## Options considered

```mermaid
flowchart TD
  q["How long do we retry a failing endpoint?"]
  q --> o0["5 attempts over about 2 hours"]
  q --> o1["8 attempts over 24 hours"]
  classDef chosen fill:#d3f9d8,stroke:#2b8a3e
  class o0 chosen
```

- **5 attempts over about 2 hours** (chosen): then the delivery shows as failed.
- **8 attempts over 24 hours**: what the delivery guarantees spec requires.[^specs-mock-2]

## Reasons

- Endpoints that are down for a day keep 8 retries each in the queue and fill it.[^discussions-mock-4]

## Consequences

- This contradicts Webhook delivery guarantees, which still says 8 retries over 24 hours. Tomás said he would update it.[^discussions-mock-4][^specs-mock-2]
- Customers whose endpoint is down for more than 2 hours lose those events unless they resend them.

## Who decided

Jonah Park and Tomás Silva, on 17 October 2026.
