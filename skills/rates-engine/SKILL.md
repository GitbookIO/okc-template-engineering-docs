---
name: rates-engine
description: How to change the Rates Engine safely. Use when working on rate quotes, the rate cache, carrier request batching or carrier request logging.
type: Skill
system: /systems/rates-engine.md
status: draft
sources:
  - id: systems-rates-engine
    resource: /systems/rates-engine.md
    title: "Rates Engine"
  - id: specs-mock-3
    resource: /specs/mock-3.md
    title: "Rate quotes under 300 ms"
  - id: prs-mock-7
    resource: /prs/mock-7.md
    title: "Cache carrier rates for an hour"
  - id: prs-mock-8
    resource: /prs/mock-8.md
    title: "Batch carrier rate requests for multi-parcel shipments"
  - id: prs-mock-15
    resource: /prs/mock-15.md
    title: "Redact carrier credentials from logs"
  - id: decisions-2026-10-27-cache-carrier-rates-for-an-hour
    resource: /decisions/2026-10-27-cache-carrier-rates-for-an-hour.md
    title: "Cache carrier rates for an hour"
generated:
  by: workflow:system-skills:anthropic/claude-opus-5-5
  at: 2026-11-09T07:00:00Z
---

## What it is

The Rates Engine quotes carrier rates for a shipment in under 300 ms at p95, by caching carrier rates and batching carrier calls. Customers' checkout pages call it on every change to an address form.[^systems-rates-engine]

## Rules from specs

- Open drift: Rate quotes under 300 ms requires cached rates to expire after 15 minutes, but they're cached for 60, as Shipping Core decided on 27 October. Don't shorten or lengthen the cache without Ana Kovac.[^specs-mock-3][^prs-mock-7][^decisions-2026-10-27-cache-carrier-rates-for-an-hour]
- p95 quote latency stays under 300 ms, including multi-parcel shipments.[^specs-mock-3]
- Never quote a cached rate after a carrier announces a price change. Price-change notices must keep clearing the cache.[^specs-mock-3][^prs-mock-7]

## How changes are made here

- Cache times live in `config/cache.yaml`.[^prs-mock-7]
- Carrier calls for one shipment go out as one batch, from `src/carriers/batch.ts`.[^prs-mock-8]
- Carrier request logging goes through `src/carriers/logging.ts`, which strips credentials and has its own tests.[^prs-mock-15]

## Before you merge

- Measure p95 for shipments with five or more parcels. They were at 1.4 seconds before batching.[^prs-mock-8]
- Never log a carrier request without going through the redacting logger. Carrier keys leaked into logs on 18 October.[^prs-mock-15]
