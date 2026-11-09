# Decisions

- [Fail over to a backup carrier for labels](2026-11-03-carrier-failover-for-labels.md): Proposed: switch a service to its backup carrier automatically when a carrier fails.
- [Launch the delivery log with 7 days](2026-10-30-launch-the-delivery-log-with-7-days.md): The dashboard delivery log launches with 7 days of attempts and a status filter, and goes to 30 days later.
- [Partition webhook delivery by shipment](2026-10-28-partition-webhook-delivery-by-shipment.md): Events for one shipment go through one partition, so they arrive in order while delivery stays parallel.
- [Cache carrier rates for an hour](2026-10-27-cache-carrier-rates-for-an-hour.md): Carrier rates stay cached for 60 minutes to cut carrier API cost, against the 15 minutes the quotes PRD sets.
- [Time out carrier label calls after 8 seconds](2026-10-24-time-out-carrier-label-calls-after-8-seconds.md): Label calls to carriers give up after 8 seconds, with a circuit breaker to follow.
- [Show a webhook delivery log in the dashboard](2026-10-20-webhook-delivery-log-in-the-dashboard.md): Customers see 30 days of delivery attempts, filter them, and resend failed events.
- [Cap webhook retries at 5 attempts](2026-10-17-cap-webhook-retries-at-5.md): Failed deliveries stop after 5 attempts over about 2 hours, instead of 8 over 24 hours.
- [Use idempotency keys for charges](2026-10-12-use-idempotency-keys-for-charges.md): Charges carry an idempotency key, and the ledger records one entry per key, so retries never charge twice.
- [Page list shipments with a cursor](2026-10-09-cursor-pagination-for-list-shipments.md): List shipments pages with an opaque cursor, 50 by default and 200 at most.
- [Quote rates in under 300 ms](2026-10-06-quote-rates-under-300-ms.md): Rate quotes stay under 300 ms at p95, with carrier rates cached for at most 15 minutes.
- [Deliver webhooks at least once, in order per shipment](2026-10-02-deliver-webhooks-at-least-once-in-order.md): The delivery guarantees customers can build on: at least once, ordered per shipment, retried, signed.
