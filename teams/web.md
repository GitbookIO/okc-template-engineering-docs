---
type: Team
title: Web
description: Owns the customer dashboard.
lead: Priya Raman
channel: '#team-web'
systems: [/systems/customer-dashboard.md]
sources:
  - id: systems-customer-dashboard
    resource: /systems/customer-dashboard.md
    title: Customer Dashboard
generated:
  by: workflow:update-teams:anthropic/claude-opus-5-5
  at: 2026-11-07T12:00:00Z
stale_after: 2026-12-07T12:00:00Z
---

Web owns the Customer Dashboard, where customers manage shipments, billing and webhooks. This month it shipped a webhook delivery log so customers can fix their own endpoints.

## Systems

- [Customer Dashboard](/systems/customer-dashboard.md): production.[^systems-customer-dashboard]

## What's changing

- The webhook settings page lists delivery attempts from the last 7 days and resends failed events.[^systems-customer-dashboard]

## Needs attention

- The delivery log drifts from its PRD: it shows 7 days instead of 30, and has no event type filter.[^systems-customer-dashboard]
