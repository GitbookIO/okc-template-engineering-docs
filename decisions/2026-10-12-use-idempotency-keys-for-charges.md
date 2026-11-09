---
type: Decision
title: Use idempotency keys for charges
description: "Charges carry an idempotency key, and the ledger records one entry per key, so retries never charge twice."
state: accepted
decided_on: 2026-10-12
deciders: [Maya Chen, Dev Okafor, Ana Kovac]
systems: [/systems/billing-api.md, /systems/ledger.md]
sources:
  - id: discussions-mock-1
    resource: /discussions/mock-1.md
    title: "How do we stop double charges?"
  - id: specs-mock-1
    resource: /specs/mock-1.md
    title: "Idempotent charges"
generated:
  by: workflow:record-decisions:anthropic/claude-opus-5-5
  at: 2026-10-14T17:00:00Z
stale_after: 2027-04-12T17:00:00Z
verified:
  - by: human:maya@acme.example
    at: 2026-10-15T09:30:00Z
---

## Decision

Every charge carries an idempotency key built from the label purchase ID, retries reuse it, and the ledger refuses a second entry for the same key.[^discussions-mock-1][^specs-mock-1]

## Options considered

```mermaid
flowchart TD
  q["How do we stop double charges?"]
  q --> o0["Idempotency keys"]
  q --> o1["Processor-side dedupe"]
  q --> o2["Lock per label purchase"]
  classDef chosen fill:#d3f9d8,stroke:#2b8a3e
  class o0 chosen
```

- **Idempotency keys** (chosen): on every charge, reused on retries, and stored in the ledger.
- **Processor-side dedupe**: needs a contract change with the processor.
- **Lock per label purchase**: doesn't help when the processor's retry and ours race.

## Reasons

- The processor already supports idempotency keys, while its own dedupe would need a contract change.[^discussions-mock-1]
- A lock on our side doesn't stop the processor's retry racing ours.[^discussions-mock-1]
- Keys in the ledger mean it refuses a second entry even if billing slips.[^discussions-mock-1]

## Consequences

- Retries are safe at the processor and in the ledger.
- The RFC also caps retries at 5 with exponential backoff.[^specs-mock-1]

## Who decided

Maya Chen, Dev Okafor and Ana Kovac, on 12 October 2026.
