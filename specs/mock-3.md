---
type: Spec
title: Rate quotes under 300 ms
resource: 'mock://specs/3'
kind: prd
state: approved
author: Ana Kovac
systems: [/systems/rates-engine.md]
approved_at: '2026-10-06T10:00:00Z'
---

## Goal

Checkout pages call us for rates on every keystroke in the address form. Slow quotes cost our customers sales.

## Requirements

- p95 quote latency stays under 300 ms, including multi-parcel shipments.
- Cached carrier rates expire after 15 minutes.
- A cached rate is never quoted after the carrier announces a price change.
