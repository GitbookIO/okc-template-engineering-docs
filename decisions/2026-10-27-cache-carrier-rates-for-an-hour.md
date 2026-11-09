---
type: Decision
title: Cache carrier rates for an hour
description: "Carrier rates stay cached for 60 minutes to cut carrier API cost, against the 15 minutes the quotes PRD sets."
state: accepted
decided_on: 2026-10-27
deciders: [Lena Ito, Ravi Menon, Ana Kovac]
systems: [/systems/rates-engine.md]
sources:
  - id: discussions-mock-3
    resource: /discussions/mock-3.md
    title: "Rate cache TTL"
  - id: specs-mock-3
    resource: /specs/mock-3.md
    title: "Rate quotes under 300 ms"
generated:
  by: workflow:record-decisions:anthropic/claude-opus-5-5
  at: 2026-10-27T16:00:00Z
stale_after: 2027-04-25T16:00:00Z
---

## Decision

Carrier rates are cached for 60 minutes. Price-change notices still clear the cache right away.[^discussions-mock-3]

## Options considered

```mermaid
flowchart TD
  q["How long do we cache carrier rates?"]
  q --> o0["60 minutes"]
  q --> o1["15 minutes"]
  classDef chosen fill:#d3f9d8,stroke:#2b8a3e
  class o0 chosen
```

- **60 minutes** (chosen): about 70 percent fewer carrier calls. Watch quote accuracy for two weeks.
- **15 minutes**: what Rate quotes under 300 ms requires.[^specs-mock-3]

## Reasons

- Carrier rate calls are the team's second largest infra cost, and an hour cuts them by about 70 percent.[^discussions-mock-3]
- Price-change notices still clear the cache, so the risk is only rate updates carriers don't announce.[^discussions-mock-3]

## Consequences

- This contradicts Rate quotes under 300 ms, which still says 15 minutes. Ana will update it after two weeks of numbers.[^discussions-mock-3][^specs-mock-3]

## Who decided

Lena Ito, Ravi Menon and Ana Kovac, on 27 October 2026.
