---
type: System
title: Customer Dashboard
description: Web app where customers manage shipments, billing and webhooks.
team: /teams/web.md
lifecycle: production
depends_on: [/systems/shipments-api.md, /systems/billing-api.md, /systems/webhooks.md]
repository: acme/customer-dashboard
specs: [/specs/mock-5.md]
sources:
  - id: prs-mock-12
    resource: /prs/mock-12.md
    title: "Show delivery attempts on the webhook settings page"
  - id: issues-mock-8
    resource: /issues/mock-8.md
    title: "Webhook settings don't show failed deliveries"
  - id: issues-mock-9
    resource: /issues/mock-9.md
    title: "Billing page times out for accounts with many labels"
  - id: incidents-mock-7
    resource: /incidents/mock-7.md
    title: "Dashboard login loop for some accounts"
  - id: specs-mock-5
    resource: /specs/mock-5.md
    title: "Webhook delivery log in the dashboard"
generated:
  by: workflow:update-systems:anthropic/claude-opus-5-5
  at: 2026-11-07T11:00:00Z
stale_after: 2026-12-07T11:00:00Z
---

The Customer Dashboard is the web app where customers manage shipments, billing and webhook settings. It reads from the Shipments API, the Billing API and Webhooks.

## Owner and dependencies

Owned by [Web](/teams/web.md).

```mermaid
flowchart LR
  customer_dashboard["Customer Dashboard"]
  customer_dashboard --> shipments_api["Shipments API"]
  customer_dashboard --> billing_api["Billing API"]
  customer_dashboard --> webhooks["Webhooks"]
```

## Recent changes

- The webhook settings page lists delivery attempts from the last 7 days, filters them by status, and resends a failed event.[^prs-mock-12]

## Open issues

- Billing page times out for accounts with many labels (ENG-240, high).[^issues-mock-9]

## Incidents

- 7 October: some customers were sent back to the login page after signing in, for 40 minutes. The cause is unknown.[^incidents-mock-7]

## Drift from spec

- Webhook delivery log in the dashboard requires 30 days of delivery attempts. The settings page shows the last 7 days.[^specs-mock-5][^prs-mock-12]
- It also requires a filter by event type. The page filters by status only.[^specs-mock-5][^prs-mock-12]

## Activity

```vega-lite
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "Issues opened per week: Customer Dashboard",
  "data": {
    "values": [
      { "week": "2026-09-28", "issues": 0 },
      { "week": "2026-10-05", "issues": 0 },
      { "week": "2026-10-12", "issues": 0 },
      { "week": "2026-10-19", "issues": 1 },
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
