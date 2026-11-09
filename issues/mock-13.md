---
type: Issue
title: Webhook signatures fail for payloads with emoji
resource: 'mock://issues/13'
identifier: ENG-243
state: backlog
priority: medium
labels: [bug, webhooks]
system: /systems/webhooks.md
team: /teams/platform.md
created_at: '2026-11-07T08:00:00Z'
updated_at: '2026-11-07T08:00:00Z'
---

A customer's signature check fails for shipments whose notes contain emoji. We seem to sign a re-encoded body instead of the bytes we send.
