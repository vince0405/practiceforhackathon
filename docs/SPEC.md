# Spec: RPS1 Farmer Booking MVP

## Problem

Farmers bringing palay to a rural rice mill need a simple way to request
processing and check that their request was received. This is a product
hypothesis from the team's brief, not yet validated through an interview with
a named farmer.

## Solution

A farmer signs in, submits a service booking with basic intake details, and
returns later to see the booking and its current status. The app keeps each
farmer's bookings private from other farmers.

## The user

One user type: a farmer booking services at the rice mill.

## User stories

1. As a farmer, I want to create an account and sign in so that my bookings
   are private to me.
2. As a farmer, I want to choose a service path so that the mill knows what
   processing I am requesting.
3. As a farmer, I want to enter my name and basic palay details so that the
   mill can identify and review my request.
4. As a farmer, I want to submit a booking and receive a clear confirmation
   so that I know the request was saved.
5. As a farmer, I want to see a list of my bookings and their statuses so
   that I can check progress later.
6. As a farmer, I want to be unable to see another farmer's bookings so
   that my information stays private.

## Screens

- **Sign in / create account**: Email and password form using Supabase Auth.
- **My bookings**: List of the signed-in farmer's bookings, service paths,
  submission times, and current statuses; an empty state links to booking.
- **New booking**: Form for customer name/contact, service path, sacks,
  estimated total weight, variety, and optional notes, with validation and a
  review/submit action.
- **Booking confirmation**: Confirms the booking was saved and links to the
  farmer's booking list.

## Data

- **profiles**: `id` (auth user ID), `full_name`, `phone`, `role`,
  `created_at`. A signed-in user may read their own profile; profile creation
  is tied to account creation. The farmer cannot change their role.
- **customers**: `id`, `profile_id`, `name`, `contact`, `address`,
  `created_at`. A farmer may create and read only customer rows whose
  `profile_id` is their own auth user ID. No farmer may read another farmer's
  customer rows.
- **jobs**: `id`, `code`, `customer_id`, `service_path`, `status`,
  `started_at`, `created_by`, `notes`, and `created_at`. A farmer may create
  a job only for a customer row they own and may read only jobs attached to
  their own customer rows. New jobs start with `status = intake`; farmers
  cannot change status or assign a different owner. Staff job updates are
  out of scope for this MVP.

Enable Row Level Security on every table and use explicit policies. Do not
expose pricing or report data to farmers. Never trust a submitted customer
or owner ID without checking it against the authenticated user.

## Login

Accounts are required. Use Supabase Auth with email and password. The user's
role in this MVP is farmer; there is no role selector or staff account
management.

## Done for the demo

- The starter remains deployed on the live Vercel URL.
- A farmer can create an account, sign in, submit a valid service booking,
  and see it after refreshing.
- Invalid or incomplete booking details are rejected with a clear message.
- A second farmer account cannot list or fetch the first farmer's customer
  or booking rows.
- RLS is enabled and has explicit policies for each table used.
- The team has shown the flow to a real farmer and recorded whether the
  hypothesis matches their needs; until then, product validation remains
  incomplete.

## Out of scope

Operator intake and stage updates; drying/milling records; warehouse
management and expiry alerts; invoices, payments, receipts, and payment
providers; admin screens, staff roles, pricing, and reports; offline writes,
PWA/service-worker caching, and sync; storage/realtime integration checks;
and multi-role Playwright flows. Track these as later work and add them only
after the booking MVP is working and reviewed.

## Assumptions and setup dependencies

- The service paths are the four options in the team's brief: package,
  drying only, drying then milling, and milling only.
- A booking is a request, not an accepted job, quote, or payment.
- The initial status is `intake`; no staff member updates it in this MVP.
- A hosted Supabase project and Vercel project are configured by the team.
- Email confirmation behavior depends on Supabase Auth settings; the demo
  must use the project's configured sign-up flow.
- No payment gateway, SMTP provider, or private server key is required for
  this MVP.
