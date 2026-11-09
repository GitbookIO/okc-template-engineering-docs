---
type: Decision
title: Page list shipments with a cursor
description: "List shipments pages with an opaque cursor, 50 by default and 200 at most."
state: accepted
decided_on: 2026-10-09
deciders: [Lena Ito]
systems: [/systems/shipments-api.md]
sources:
  - id: specs-mock-6
    resource: /specs/mock-6.md
    title: "Cursor pagination for list shipments"
generated:
  by: workflow:record-decisions:anthropic/claude-opus-5-5
  at: 2026-10-09T15:00:00Z
stale_after: 2027-04-07T15:00:00Z
---

## Decision

GET /v1/shipments pages with an opaque cursor. The default page size is 50, the maximum is 200, and filters from the first request apply to every page.[^specs-mock-6]

## Options considered

```mermaid
flowchart TD
  q["How does list shipments page?"]
  q --> o0["Opaque cursor"]
  q --> o1["Offset and limit"]
  classDef chosen fill:#d3f9d8,stroke:#2b8a3e
  class o0 chosen
```

- **Opaque cursor** (chosen): default page size 50, maximum 200, filters apply to every page.
- **Offset and limit**: keeps working until v1 is retired.

## Reasons

- The design gives no reasons beyond the requirements themselves.[^specs-mock-6]

## Consequences

- Offset pagination stays until v1 is retired.[^specs-mock-6]

## Who decided

Lena Ito, on 9 October 2026.
