---
type: Decision
title: Quote rates in under 300 ms
description: "Rate quotes stay under 300 ms at p95, with carrier rates cached for at most 15 minutes."
state: accepted
decided_on: 2026-10-06
deciders: [Ana Kovac]
systems: [/systems/rates-engine.md]
sources:
  - id: specs-mock-3
    resource: /specs/mock-3.md
    title: "Rate quotes under 300 ms"
generated:
  by: workflow:record-decisions:anthropic/claude-opus-5-5
  at: 2026-10-06T11:00:00Z
stale_after: 2027-04-04T11:00:00Z
---

## Decision

Quotes stay under 300 ms at p95, including multi-parcel shipments. Cached carrier rates expire after 15 minutes, and a cached rate is never quoted after a carrier announces a price change.[^specs-mock-3]

## Options considered

```mermaid
flowchart TD
  q["How fast must quotes be, and how fresh?"]
  q --> o0["Under 300 ms, rates cached at most 15 minutes"]
  classDef chosen fill:#d3f9d8,stroke:#2b8a3e
  class o0 chosen
```

- **Under 300 ms, rates cached at most 15 minutes** (chosen): never quote a rate after a carrier announces a price change. The PRD names no other option.

## Reasons

- Checkout pages call for rates on every keystroke in the address form, and slow quotes cost customers sales.[^specs-mock-3]

## Consequences

- The Rates Engine needs a cache and batched carrier calls to hit 300 ms.
- A later decision raised the cache time to 60 minutes. See [Cache carrier rates for an hour](2026-10-27-cache-carrier-rates-for-an-hour.md).

## Who decided

Ana Kovac, on 6 October 2026.
