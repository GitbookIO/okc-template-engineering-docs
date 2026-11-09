---
type: Pull Request
title: Restart stalled carrier feed pollers
resource: 'mock://prs/10'
state: merged
number: 74
repository: acme/tracking-events
author: jonah-park
merged_at: '2026-10-31T12:45:00Z'
systems: [/systems/tracking-events.md]
---

A poller that gets an auth error now refreshes its token and restarts, instead of retrying the same request forever. That is what kept one carrier's updates two hours late on 30 October.

## Changed files

- `src/pollers/runner.ts`
- `src/pollers/auth.ts`
