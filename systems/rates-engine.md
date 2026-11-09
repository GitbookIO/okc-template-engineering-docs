---
type: System
title: Rates Engine
description: Quotes carrier rates for a shipment and caches them.
team: /teams/shipping-core.md
lifecycle: production
depends_on: []
repository: acme/rates-engine
specs: [/specs/mock-3.md]
sources:
  - id: prs-mock-7
    resource: /prs/mock-7.md
    title: "Cache carrier rates for an hour"
  - id: prs-mock-15
    resource: /prs/mock-15.md
    title: "Redact carrier credentials from logs"
  - id: prs-mock-8
    resource: /prs/mock-8.md
    title: "Batch carrier rate requests for multi-parcel shipments"
  - id: issues-mock-5
    resource: /issues/mock-5.md
    title: "Quotes are slow for multi-parcel shipments"
  - id: issues-mock-12
    resource: /issues/mock-12.md
    title: "Rates engine logs carrier API keys"
  - id: specs-mock-3
    resource: /specs/mock-3.md
    title: "Rate quotes under 300 ms"
  - id: specs-mock-7
    resource: /specs/mock-7.md
    title: "Carrier rate card imports"
generated:
  by: workflow:update-systems:anthropic/claude-opus-5-5
  at: 2026-11-05T12:00:00Z
stale_after: 2026-12-05T12:00:00Z
---

The Rates Engine quotes carrier rates for a shipment, in under 300 ms at p95, by caching carrier rates and batching carrier calls. Customers' checkout pages call it on every change to an address form.

## Owner and dependencies

Owned by [Shipping Core](/teams/shipping-core.md). It depends on no other Acme system.

```mermaid
flowchart LR
  rates_engine["Rates Engine"]
```

## Recent changes

- Carrier rates are cached for 60 minutes instead of 15. Price-change notices still clear the cache right away.[^prs-mock-7]
- Carrier credentials are no longer written to logs, and the two exposed keys are rotated.[^prs-mock-15]
- Rates for all parcels in a shipment go to the carrier in one batch, which brought multi-parcel quotes from 1.4 seconds to 280 ms.[^prs-mock-8]

## Open issues

None.

## Incidents

None in the last 90 days.

## Drift from spec

- Rate quotes under 300 ms requires cached rates to expire after 15 minutes. Rates are now cached for 60 minutes.[^specs-mock-3][^prs-mock-7]

## Activity

```vega-lite
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "Issues opened per week: Rates Engine",
  "data": {
    "values": [
      { "week": "2026-09-28", "issues": 0 },
      { "week": "2026-10-05", "issues": 1 },
      { "week": "2026-10-12", "issues": 1 },
      { "week": "2026-10-19", "issues": 0 },
      { "week": "2026-10-26", "issues": 0 },
      { "week": "2026-11-02", "issues": 0 }
    ]
  },
  "mark": "bar",
  "encoding": {
    "x": { "field": "week", "type": "ordinal", "title": "Week of" },
    "y": {
      "field": "issues",
      "type": "quantitative",
      "title": "Issues opened",
      "axis": {
        "tickMinStep": 1
      }
    }
  }
}
```
