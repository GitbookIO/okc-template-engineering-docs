---
type: System
title: Billing API
description: Charges customers for labels and retries failed charges.
team: /teams/payments.md
lifecycle: production
depends_on: [/systems/ledger.md]
repository: acme/billing-api
specs: [/specs/mock-1.md]
runbooks: [/runbooks/duplicate-charges.md]
sources:
  - id: prs-mock-16
    resource: /prs/mock-16.md
    title: "Store processor response codes on failed charges"
  - id: prs-mock-2
    resource: /prs/mock-2.md
    title: "Retry failed charges with a fixed delay"
  - id: prs-mock-1
    resource: /prs/mock-1.md
    title: "Add idempotency keys to charge requests"
  - id: issues-mock-1
    resource: /issues/mock-1.md
    title: "Label charges retried twice after a processor timeout"
  - id: issues-mock-3
    resource: /issues/mock-3.md
    title: "Invoice PDFs show charge times in UTC"
  - id: incidents-mock-1
    resource: /incidents/mock-1.md
    title: "Customers charged twice for one label"
  - id: specs-mock-1
    resource: /specs/mock-1.md
    title: "Idempotent charges"
generated:
  by: workflow:update-systems:anthropic/claude-opus-5-5
  at: 2026-11-03T16:00:00Z
stale_after: 2026-12-03T16:00:00Z
verified:
  - by: human:maya@acme.example
    at: 2026-11-04T09:00:00Z
---

The Billing API charges customers for every label they buy and retries charges that fail. Label Service calls it on each purchase, and the Customer Dashboard reads charges from it for the billing page.

## Owner and dependencies

Owned by [Payments](/teams/payments.md).

```mermaid
flowchart LR
  billing_api["Billing API"]
  billing_api --> ledger["Ledger"]
```

## Recent changes

- Failed charges keep the processor's response code and message, so support can tell a declined card from a processor error.[^prs-mock-16]
- Failed charges are retried 3 times, 10 seconds apart, then marked failed.[^prs-mock-2]
- Every charge carries an idempotency key built from the label purchase ID, so a retry can't charge twice.[^prs-mock-1]

## Open issues

- Invoice PDFs show charge times in UTC (ENG-231, low).[^issues-mock-3]

## Incidents

- 2 October: fourteen accounts were charged twice for one label after processor timeouts. See [Duplicate charges](/runbooks/duplicate-charges.md).[^incidents-mock-1]

## Drift from spec

- Idempotent charges requires at most 5 retries with exponential backoff starting at 2 seconds. Retries now stop after 3 attempts, 10 seconds apart.[^specs-mock-1][^prs-mock-2]

## Activity

```vega-lite
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "Issues opened per week: Billing API",
  "data": {
    "values": [
      { "week": "2026-09-28", "issues": 1 },
      { "week": "2026-10-05", "issues": 0 },
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
