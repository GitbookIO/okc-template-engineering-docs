---
type: Spec
title: Idempotent charges
resource: 'mock://specs/1'
kind: rfc
state: approved
author: Maya Chen
systems: [/systems/billing-api.md]
approved_at: '2026-10-14T16:00:00Z'
---

## Problem

A charge that times out can't be retried safely. On 2 October fourteen accounts were charged twice.

## Proposal

- Every charge request carries an idempotency key built from the label purchase ID.
- Every retry reuses the key.
- A failed charge is retried at most 5 times, with exponential backoff starting at 2 seconds.
- The ledger records one entry per key.

## Out of scope

Refund flows, which already carry their own keys.
