---
type: Pull Request
title: Show delivery attempts on the webhook settings page
resource: 'mock://prs/12'
state: merged
number: 318
repository: acme/customer-dashboard
author: sofia-lund
merged_at: '2026-11-07T10:30:00Z'
issues: [/issues/mock-8.md]
systems: [/systems/customer-dashboard.md]
---

The webhook settings page now lists delivery attempts from the last 7 days, with a filter by status and a button to resend a failed event. Thirty days of attempts made the query too slow for launch.

Fixes ENG-237.

## Changed files

- `app/settings/webhooks/attempts.tsx`
- `app/settings/webhooks/resend.ts`
