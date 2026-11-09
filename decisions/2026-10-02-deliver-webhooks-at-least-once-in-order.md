---
type: Decision
title: Deliver webhooks at least once, in order per shipment
description: "The delivery guarantees customers can build on: at least once, ordered per shipment, retried, signed."
state: accepted
decided_on: 2026-10-02
deciders: [Tomás Silva]
systems: [/systems/webhooks.md]
sources:
  - id: specs-mock-2
    resource: /specs/mock-2.md
    title: "Webhook delivery guarantees"
generated:
  by: workflow:record-decisions:anthropic/claude-opus-5-5
  at: 2026-10-02T13:00:00Z
stale_after: 2027-03-31T13:00:00Z
---

## Decision

Webhooks are delivered at least once, events for one shipment arrive in the order they happened, failed deliveries are retried up to 8 times over 24 hours, and every payload is signed.[^specs-mock-2]

## Options considered

```mermaid
flowchart TD
  q["What does webhook delivery guarantee?"]
  q --> o0["At least once, ordered per shipment"]
  q --> o1["Exactly once"]
  q --> o2["Best effort"]
  classDef chosen fill:#d3f9d8,stroke:#2b8a3e
  class o0 chosen
```

- **At least once, ordered per shipment** (chosen): retried up to 8 times over 24 hours, signed over the exact bytes sent.
- **Exactly once**: the spec doesn't weigh it.
- **Best effort**: the spec doesn't weigh it.

## Reasons

- Customers build shipment timelines from these events and verify every payload, and both break if delivery reorders or re-encodes.[^specs-mock-2]

## Consequences

- Delivery has to keep order within a shipment, which limits how it can run in parallel.
- Customers must handle a repeated event.

## Who decided

Tomás Silva, on 2 October 2026.
