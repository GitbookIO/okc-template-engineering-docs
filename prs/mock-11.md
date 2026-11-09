---
type: Pull Request
title: Store raw carrier events for replay
resource: 'mock://prs/11'
state: merged
number: 79
repository: acme/tracking-events
author: tomas-silva
merged_at: '2026-11-06T14:00:00Z'
systems: [/systems/tracking-events.md]
---

Every raw carrier event is now stored for 14 days before it is parsed. When a parser bug or an outage drops updates, we can replay them into shipment timelines.

## Changed files

- `src/ingest/raw-store.ts`
- `scripts/replay.ts`
