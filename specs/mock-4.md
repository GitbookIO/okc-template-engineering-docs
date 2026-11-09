---
type: Spec
title: Carrier failover for labels
resource: 'mock://specs/4'
kind: rfc
state: in review
author: Lena Ito
systems: [/systems/label-service.md]
---

## Problem

Twice in two weeks a carrier's label API failed and someone had to set `labels.carrier_override` by hand.

## Options

1. A backup carrier per service, used automatically when the circuit breaker opens.
2. Queue the purchase and retry it when the carrier recovers.
3. Fail fast and let the customer choose another service.

## Open questions

- Which price do we charge when the backup carrier costs more?
- Do customers need to opt in?
