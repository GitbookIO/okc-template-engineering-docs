---
type: Decision
title: Partition webhook delivery by shipment
description: "Events for one shipment go through one partition, so they arrive in order while delivery stays parallel."
state: accepted
decided_on: 2026-10-28
deciders: [Tomás Silva, Jonah Park, Priya Raman]
systems: [/systems/webhooks.md]
sources:
  - id: discussions-mock-2
    resource: /discussions/mock-2.md
    title: "Fixing out-of-order webhooks"
generated:
  by: workflow:record-decisions:anthropic/claude-opus-5-5
  at: 2026-10-28T14:00:00Z
stale_after: 2027-04-26T14:00:00Z
---

## Decision

The delivery queue is partitioned by shipment ID, and one worker consumes each partition in order.[^discussions-mock-2]

## Options considered

```mermaid
flowchart TD
  q["How do we fix out-of-order webhooks?"]
  q --> o0["Partition the queue by shipment"]
  q --> o1["Sequence numbers, customers reorder"]
  q --> o2["Back to one consumer"]
  classDef chosen fill:#d3f9d8,stroke:#2b8a3e
  class o0 chosen
```

- **Partition the queue by shipment** (chosen): ordered within a shipment, parallel across shipments.
- **Sequence numbers, customers reorder**: pushes the work onto every customer.
- **Back to one consumer**: brings back the 14 October backlog.

## Reasons

- Sequence numbers push the work onto every customer.[^discussions-mock-2]
- One consumer can't keep up with bursts.[^discussions-mock-2]
- Per-shipment order also makes the dashboard delivery log easier.[^discussions-mock-2]

## Consequences

- Delivery keeps the order the delivery guarantees spec requires.

## Who decided

Tomás Silva, Jonah Park and Priya Raman, on 28 October 2026.
