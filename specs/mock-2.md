---
type: Spec
title: Webhook delivery guarantees
resource: 'mock://specs/2'
kind: tdd
state: approved
author: 'Tomás Silva'
systems: [/systems/webhooks.md]
approved_at: '2026-10-02T12:00:00Z'
---

## Guarantees

- Every event is delivered at least once.
- Events for the same shipment are delivered in the order they happened.
- A failed delivery is retried up to 8 times over 24 hours, with exponential backoff.
- Each payload is signed with HMAC SHA-256 over the exact bytes sent, in the `Acme-Signature` header.

## Why

Customers build shipment timelines from our events and verify every payload. Both break if we reorder or re-encode.
