---
type: Decision
title: Time out carrier label calls after 8 seconds
description: "Label calls to carriers give up after 8 seconds, with a circuit breaker to follow."
state: accepted
decided_on: 2026-10-24
deciders: [Lena Ito, Ravi Menon, Jonah Park]
systems: [/systems/label-service.md]
sources:
  - id: discussions-mock-8
    resource: /discussions/mock-8.md
    title: "Carrier timeouts"
generated:
  by: workflow:record-decisions:anthropic/claude-opus-5-5
  at: 2026-10-24T15:00:00Z
stale_after: 2027-04-22T15:00:00Z
---

## Decision

Carrier label calls time out after 8 seconds and return a retryable error. A circuit breaker follows.[^discussions-mock-8]

## Options considered

```mermaid
flowchart TD
  q["How do we stop a slow carrier from blocking every label?"]
  q --> o0["8 second timeout now, circuit breaker next"]
  q --> o1["Circuit breaker only"]
  classDef chosen fill:#d3f9d8,stroke:#2b8a3e
  class o0 chosen
```

- **8 second timeout now, circuit breaker next** (chosen): the timeout ships the same day.
- **Circuit breaker only**: takes longer to build.

## Reasons

- Label calls had no timeout, so every worker was stuck on one carrier.[^discussions-mock-8]
- Carrier p99 is about 3 seconds, so 8 seconds leaves room.[^discussions-mock-8]

## Consequences

- One slow carrier no longer holds every worker, but its purchases still fail until someone switches carriers.

## Who decided

Lena Ito, Ravi Menon and Jonah Park, on 24 October 2026.
