---
name: billing-api
description: How to change the Billing API safely. Use when working on charges, charge retries, idempotency keys or charge failure codes.
type: Skill
system: /systems/billing-api.md
sources:
  - id: systems-billing-api
    resource: /systems/billing-api.md
    title: "Billing API"
  - id: specs-mock-1
    resource: /specs/mock-1.md
    title: "Idempotent charges"
  - id: prs-mock-1
    resource: /prs/mock-1.md
    title: "Add idempotency keys to charge requests"
  - id: prs-mock-2
    resource: /prs/mock-2.md
    title: "Retry failed charges with a fixed delay"
  - id: prs-mock-16
    resource: /prs/mock-16.md
    title: "Store processor response codes on failed charges"
  - id: incidents-mock-1
    resource: /incidents/mock-1.md
    title: "Customers charged twice for one label"
  - id: runbooks-duplicate-charges
    resource: /runbooks/duplicate-charges.md
    title: "Duplicate charges"
generated:
  by: workflow:system-skills:anthropic/claude-opus-5-5
  at: 2026-11-09T07:00:00Z
---

## What it is

The Billing API charges customers for every label they buy and retries charges that fail. Label Service calls it on each purchase.[^systems-billing-api]

## Rules from specs

- Open drift: Idempotent charges requires at most 5 retries with exponential backoff from 2 seconds, but retries now stop after 3, 10 seconds apart. Check with Payments before changing retry timing.[^specs-mock-1][^prs-mock-2]
- Every charge request carries an idempotency key built from the label purchase ID.[^specs-mock-1]
- Every retry reuses that key.[^specs-mock-1]
- The ledger records one entry per key.[^specs-mock-1]

## How changes are made here

- Charge logic lives in `src/charges/`, and retry behaviour is tested in `test/charges/retry.test.ts`.[^prs-mock-1][^prs-mock-2]
- Schema changes are numbered SQL files in `migrations/`.[^prs-mock-16]
- Pull request descriptions name the issue they fix and the spec they follow.[^prs-mock-1]

## Before you merge

- Run the retry tests with a processor timeout. A timeout is what charged fourteen accounts twice.[^incidents-mock-1]
- Make sure the change can't write a second ledger entry for one charge.[^runbooks-duplicate-charges]
- If double charges show up after a deploy, pause the charge retry job first.[^runbooks-duplicate-charges]
