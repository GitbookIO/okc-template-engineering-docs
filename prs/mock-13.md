---
type: Pull Request
title: Validate postal codes before creating shipments
resource: 'mock://prs/13'
state: merged
number: 540
repository: acme/shipments-api
author: ravi-menon
merged_at: '2026-10-15T09:00:00Z'
issues: [/issues/mock-10.md]
systems: [/systems/shipments-api.md]
---

Addresses without a postal code are accepted for countries that don't use them. Where one is required and missing, the API returns a 422 that names the field.

Fixes ENG-221.

## Changed files

- `src/addresses/validate.ts`
- `test/addresses/postal-code.test.ts`
