# RPS1

## Who

The first intended user is a farmer who brings palay to a rural rice mill.
This is the team's target persona, not a claim that a specific farmer has
already been interviewed.

## The struggle

The team's current hypothesis is that farmers need a clearer way to request
rice-mill services and check whether a request has been received or processed.
The frequency, impact, and current status-checking experience have not yet
been confirmed with a named farmer.

## Today's workaround

Unknown. The team has not yet documented a real farmer's current process or
the time, money, or stress it costs.

## The MVP

Let a farmer sign in, submit a service booking, and see the status of only
their own bookings.

## How we'll know it worked

On the live URL, a farmer can sign in, submit one booking, refresh the page,
and still see that booking and its current status. A second farmer account
cannot see the first farmer's booking. Before treating this as a validated
product problem, ask a real farmer to try the flow and record whether it
matches their actual need.

## Out of scope

- Operator intake, weighing, and job-stage updates.
- Drying and milling production records.
- Warehouse bins, storage, expiry tracking, and stock movements.
- Invoices, payment collection, gateways, and receipts.
- Admin users, roles, pricing, settings, and reports.
- Offline writes, PWA installation, and background synchronization.
- Production connection tests and multi-role end-to-end tests.

## Glossary

- **Booking**: A farmer's request for one of the rice mill's service paths;
  it is not a confirmed price or a payment.
- **Service path**: The requested processing option: package, drying,
  drying and milling, or milling.
- **Job status**: The mill's recorded progress for a booking. In this MVP,
  the farmer can view the initial received status; staff updates come later.
