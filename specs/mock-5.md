---
type: Spec
title: Webhook delivery log in the dashboard
resource: 'mock://specs/5'
kind: prd
state: approved
author: Priya Raman
systems: [/systems/customer-dashboard.md]
approved_at: '2026-10-20T09:00:00Z'
---

## Goal

Customers fix their own webhook endpoints without writing to support.

## Requirements

- Show every delivery attempt from the last 30 days.
- Filter attempts by status and by event type.
- Resend a failed event with one click.
