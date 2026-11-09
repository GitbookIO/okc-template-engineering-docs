---
type: Team
title: Platform
description: Owns tracking events and webhook delivery.
lead: Tomás Silva
channel: '#team-platform'
systems: [/systems/tracking-events.md, /systems/webhooks.md]
sources:
  - id: systems-tracking-events
    resource: /systems/tracking-events.md
    title: Tracking Events
  - id: systems-webhooks
    resource: /systems/webhooks.md
    title: Webhooks
generated:
  by: workflow:update-teams:anthropic/claude-opus-5-5
  at: 2026-11-07T10:00:00Z
stale_after: 2026-12-07T10:00:00Z
---

Platform owns how carrier tracking updates come in and how shipment events go out to customers. This month it fixed out-of-order webhooks and made stalled carrier feeds recover on their own.

## Systems

- [Tracking Events](/systems/tracking-events.md): production.[^systems-tracking-events]
- [Webhooks](/systems/webhooks.md): production.[^systems-webhooks]

## What's changing

- Webhook events for one shipment arrive in order again, through a queue partitioned by shipment.[^systems-webhooks]
- Failed webhook deliveries stop after 5 attempts over about 2 hours.[^systems-webhooks]
- Raw carrier events are kept for 14 days so dropped updates can be replayed.[^systems-tracking-events]
- Carrier feed pollers refresh their token and restart on auth errors.[^systems-tracking-events]

## Needs attention

- Webhook retries drift from Webhook delivery guarantees, which requires 8 retries over 24 hours.[^systems-webhooks]
