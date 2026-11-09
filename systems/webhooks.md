---
type: System
title: Webhooks
description: Delivers shipment events to customer endpoints, with retries.
team: /teams/platform.md
lifecycle: production
depends_on: [/systems/tracking-events.md]
repository: acme/webhooks
specs: [/specs/mock-2.md]
runbooks: [/runbooks/webhook-delivery-backlog.md]
sources:
  - id: prs-mock-5
    resource: /prs/mock-5.md
    title: "Partition the delivery queue by shipment"
  - id: prs-mock-6
    resource: /prs/mock-6.md
    title: "Cap delivery retries at 5 attempts"
  - id: prs-mock-4
    resource: /prs/mock-4.md
    title: "Deliver retries from a parallel worker pool"
  - id: issues-mock-4
    resource: /issues/mock-4.md
    title: "Tracking webhooks arrive out of order"
  - id: issues-mock-13
    resource: /issues/mock-13.md
    title: "Webhook signatures fail for payloads with emoji"
  - id: incidents-mock-2
    resource: /incidents/mock-2.md
    title: "Webhook deliveries fell 40 minutes behind"
  - id: specs-mock-2
    resource: /specs/mock-2.md
    title: "Webhook delivery guarantees"
generated:
  by: workflow:update-systems:anthropic/claude-opus-5-5
  at: 2026-11-07T08:30:00Z
stale_after: 2026-12-07T08:30:00Z
verified:
  - by: human:tomas@acme.example
    at: 2026-11-07T15:00:00Z
---

Webhooks delivers shipment events to the endpoints customers register, signs every payload, and retries failed deliveries. Customers build their own shipment timelines from these events.

## Owner and dependencies

Owned by [Platform](/teams/platform.md).

```mermaid
flowchart LR
  webhooks["Webhooks"]
  webhooks --> tracking_events["Tracking Events"]
```

## Recent changes

- The delivery queue is partitioned by shipment, so events for one shipment arrive in order again while delivery stays parallel across shipments.[^prs-mock-5]
- Failed deliveries are retried 5 times over about 2 hours, then dropped and shown as failed.[^prs-mock-6]
- Retries go through a pool of 16 workers instead of one consumer.[^prs-mock-4]

## Open issues

- Webhook signatures fail for payloads with emoji (ENG-243, medium).[^issues-mock-13]

## Incidents

- 14 October: deliveries fell 40 minutes behind during a burst of tracking updates. See [Webhook delivery backlog](/runbooks/webhook-delivery-backlog.md).[^incidents-mock-2]

## Drift from spec

- Webhook delivery guarantees requires up to 8 retries over 24 hours. Retries now stop after 5 attempts over about 2 hours.[^specs-mock-2][^prs-mock-6]

## Activity

```vega-lite
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "Issues opened per week: Webhooks",
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
