---
type: System
title: Shipments API
description: Public API to create, list and track shipments.
team: /teams/shipping-core.md
lifecycle: production
depends_on: [/systems/rates-engine.md, /systems/label-service.md, /systems/billing-api.md, /systems/webhooks.md]
repository: acme/shipments-api
specs: [/specs/mock-6.md]
runbooks: [/runbooks/failed-migrations.md]
sources:
  - id: prs-mock-14
    resource: /prs/mock-14.md
    title: "Add cursor pagination to list shipments"
  - id: prs-mock-13
    resource: /prs/mock-13.md
    title: "Validate postal codes before creating shipments"
  - id: issues-mock-10
    resource: /issues/mock-10.md
    title: "Creating a shipment fails when the address has no postal code"
  - id: issues-mock-11
    resource: /issues/mock-11.md
    title: "List shipments ignores the status filter after the first page"
  - id: incidents-mock-6
    resource: /incidents/mock-6.md
    title: "Shipments API errors after a deploy"
  - id: specs-mock-6
    resource: /specs/mock-6.md
    title: "Cursor pagination for list shipments"
generated:
  by: workflow:update-systems:anthropic/claude-opus-5-5
  at: 2026-11-04T10:00:00Z
stale_after: 2026-12-04T10:00:00Z
verified:
  - by: process:contract-tests
    at: 2026-11-08T10:00:00Z
---

The Shipments API is Acme's public API to create, list and track shipments. It calls the Rates Engine for quotes, Label Service for labels, and the Billing API for charges, and hands events to Webhooks.

## Owner and dependencies

Owned by [Shipping Core](/teams/shipping-core.md).

```mermaid
flowchart LR
  shipments_api["Shipments API"]
  shipments_api --> rates_engine["Rates Engine"]
  shipments_api --> label_service["Label Service"]
  shipments_api --> billing_api["Billing API"]
  shipments_api --> webhooks["Webhooks"]
```

## Recent changes

- List shipments pages with an opaque cursor, 50 per page by default and 200 at most.[^prs-mock-14]
- Addresses without a postal code are accepted where countries don't use them, and a missing required one returns a 422 naming the field.[^prs-mock-13]

## Open issues

- List shipments ignores the status filter after the first page (ENG-238, medium).[^issues-mock-11]

## Incidents

- 2 November: a third of shipment creates failed for 20 minutes after a migration added a required column with no default. See [Failed migrations](/runbooks/failed-migrations.md).[^incidents-mock-6]

## Drift from spec

- No drift found against Cursor pagination for list shipments.[^specs-mock-6]

## Activity

```vega-lite
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "Issues opened per week: Shipments API",
  "data": {
    "values": [
      { "week": "2026-09-28", "issues": 0 },
      { "week": "2026-10-05", "issues": 1 },
      { "week": "2026-10-12", "issues": 0 },
      { "week": "2026-10-19", "issues": 0 },
      { "week": "2026-10-26", "issues": 0 },
      { "week": "2026-11-02", "issues": 1 }
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
