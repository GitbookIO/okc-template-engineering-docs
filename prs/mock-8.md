---
type: Pull Request
title: Batch carrier rate requests for multi-parcel shipments
resource: 'mock://prs/8'
state: merged
number: 149
repository: acme/rates-engine
author: ravi-menon
merged_at: '2026-10-13T15:10:00Z'
issues: [/issues/mock-5.md]
systems: [/systems/rates-engine.md]
---

Rates for all parcels in a shipment now go to the carrier in one batch request. p95 for five or more parcels drops from 1.4 seconds to 280 ms in staging.

Fixes ENG-228.

## Changed files

- `src/carriers/batch.ts`
- `src/quotes/quote.ts`
