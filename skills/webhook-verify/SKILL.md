---
name: webhook-verify
version: 1.0.1
description: >
  Implement or review an inbound webhook receiver: raw-body signature checks, replay protection, idempotent processing and safe retries. Use when your service accepts event callbacks from another system.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - api
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: webhook-verify
  official: true
  security_flags: []
---

# Webhook Verify

## When to use
An external sender calls your endpoint and your code acts on what it says.

## Steps
1. Read the sender's current docs: signature header, exact signed content, algorithm, encoding, timestamp, event ID, retry schedule and expected response time. Use its maintained verification library if available.
2. Get the raw request bytes before any parser. Verify the signature over exactly what the sender signed, then parse. Re-serialised JSON will not match reliably.
3. Compare with a constant-time function. Load the secret per environment from configuration, fail closed if missing, and accept two secrets during rotation.
4. Where a timestamp is part of the signature, reject values outside a short tolerance. Without one, rely on stored event IDs and fetch current state from the sender's API for sensitive actions.
5. After verification, check the event belongs to the expected account and environment.
6. Deduplicate with a unique constraint on sender plus event ID. Record the event and its work in one transaction or durably queue it, so a crash cannot mark it done without doing it.
7. Return success only after the event is durably accepted, then process slow work asynchronously. Return errors that make the sender retry on temporary failures.
8. Tolerate out-of-order and missing events: compare versions or refetch the object, and provide reconciliation.
9. Test valid, altered body, wrong secret, missing header, stale timestamp, duplicate, concurrent duplicate and reversed order.

## Watch out for
- A secret URL or source-address list alone is not authentication.
- Check-then-insert deduplication lets concurrent deliveries both run.
- Logging headers and bodies can store secrets and personal data.
- A disabled-verification flag for local testing must be impossible in production.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Forged and stale requests are rejected, a duplicated delivery produces one effect, and the tests above run against the real handler.
