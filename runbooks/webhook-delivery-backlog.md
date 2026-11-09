---
type: Runbook
title: Webhook delivery backlog
description: What to do when webhook deliveries fall behind.
system: /systems/webhooks.md
team: /teams/platform.md
sources:
  - id: incidents-mock-2
    resource: /incidents/mock-2.md
    title: Webhook deliveries fell 40 minutes behind
generated:
  by: workflow:update-runbooks:anthropic/claude-opus-5-5
  at: 2026-10-14T19:30:00Z
stale_after: 2026-11-13T19:30:00Z
---

## When to use

Customers say tracking webhooks arrive late, or the delivery queue alert fires. It has happened when a carrier sent a burst of tracking updates.[^incidents-mock-2]

## Check

1. Look at the delivery queue depth. The alert fires at 10,000 queued events.
2. Check whether one carrier is sending far more tracking updates than usual.

## Fix

1. Add consumers until the queue stops growing.[^incidents-mock-2]
2. Wait for the queue to drain, then scale back.

## Escalate

Tell [Platform](/teams/platform.md) in #team-platform if the queue is still growing 30 minutes after adding consumers.

## Past incidents

- 14 October 2026: deliveries fell 40 minutes behind during a tracking burst.[^incidents-mock-2]
