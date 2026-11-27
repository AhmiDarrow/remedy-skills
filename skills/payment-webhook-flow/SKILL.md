---
name: payment-webhook-flow
version: 1.0.1
description: >
  Keep paid access correct from payment provider events across checkout, renewal, failure, refund and cancellation. Use when granting or revoking plans or credits based on payment webhooks.
author: Remedy Official
license: Apache-2.0
tags:
  - payments
  - backend
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: payment-webhook-flow
  official: true
  security_flags: []
---

# Payment Webhook Flow

## When to use
Your product unlocks something because a payment provider says money moved. Generic signature and replay handling belongs to the webhook receiver skill; this covers entitlement state.

## Steps
1. Read the current provider documentation for the installed API version: event names, signature check on the raw body, retries and ordering. Do not rely on remembered names.
2. Write a state table: free, trialing, active, past due with grace, cancel at period end, ended, refunded, disputed. For each event give the transition and what access the user has. The owner decides grace and refund policy.
3. Link provider customer and subscription ids to your account when your server creates checkout. Do not match by email.
4. Verify, store the event id under a unique constraint, and apply the change transactionally. Mark it processed only when the effect committed, so failures are retried.
5. Assume duplicates and reordering. Where order matters, fetch the current object from the provider instead of trusting an old payload.
6. Check that product, price, amount, currency and payment status match what you grant. Completed checkout can still have payment pending for delayed methods.
7. Grant consumable credits through a ledger keyed by payment id so they cannot be added twice.
8. Treat the success redirect as display only. Add reconciliation that compares provider state with your entitlements and reports mismatches.
9. Test with the provider's test mode and keys only: each transition, duplicates, reverse order and a crash mid-handler.

## Watch out for
- Test and live events mixed in one environment.
- An old cancellation arriving late and revoking a newer subscription.
- Logging full payloads with customer details.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every row of the state table is exercised in test mode with the expected access, replaying events changes nothing, and reconciliation reports no unexplained mismatch.
