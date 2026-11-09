---
type: Decision
title: Fail over to a backup carrier for labels
description: "Proposed: switch a service to its backup carrier automatically when a carrier fails."
state: proposed
decided_on: 2026-11-03
deciders: [Lena Ito]
systems: [/systems/label-service.md]
sources:
  - id: discussions-mock-5
    resource: /discussions/mock-5.md
    title: "Carrier failover options"
  - id: specs-mock-4
    resource: /specs/mock-4.md
    title: "Carrier failover for labels"
generated:
  by: workflow:record-decisions:anthropic/claude-opus-5-5
  at: 2026-11-03T12:00:00Z
stale_after: 2027-05-02T12:00:00Z
status: draft
---

## Decision

Not decided. Lena proposes a backup carrier per service, used automatically when the circuit breaker opens. The RFC stays in review until pricing is answered.[^discussions-mock-5][^specs-mock-4]

## Options considered

```mermaid
flowchart TD
  q["What happens when a carrier fails?"]
  q --> o0["Backup carrier per service"]
  q --> o1["Queue and retry later"]
  q --> o2["Fail fast"]
```

- **Backup carrier per service**: Lena's proposal, used automatically when the circuit breaker opens.
- **Queue and retry later**: simpler, but customers want a label now.
- **Fail fast**: the customer picks another service.

## Reasons

- Twice in two weeks someone had to set the carrier override by hand.[^specs-mock-4]
- Customers want a label now, not a queued purchase.[^discussions-mock-5]

## Consequences

- Billing needs to know who pays when the backup carrier costs more.[^discussions-mock-5]

## Who decided

Lena Ito, on 3 November 2026. Nothing is agreed yet.
