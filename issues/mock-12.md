---
type: Issue
title: Rates engine logs carrier API keys
resource: 'mock://issues/12'
identifier: ENG-224
state: done
priority: urgent
assignee: Lena Ito
labels: [security]
system: /systems/rates-engine.md
team: /teams/shipping-core.md
created_at: '2026-10-18T07:50:00Z'
updated_at: '2026-10-18T13:30:00Z'
closed_at: '2026-10-18T13:30:00Z'
---

Debug logging for carrier requests writes the full request, including the carrier API key header. Keys for two carriers are in the log store. Rotate them and stop logging credentials.
