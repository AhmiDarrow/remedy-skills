---
name: retry-backoff-policy
version: 1.0.0
description: >
  Define which failed calls a service retries, how long it waits and when it gives up, without amplifying an outage. Use when adding or fixing retries around network or database calls.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - reliability
  - api
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: retry-backoff-policy
  official: true
  domain: backend
  security_flags: []
---

# Retry Backoff Policy

## When to use
Calls to another service fail intermittently, or an incident showed retries piling load onto something already struggling.

## Steps
1. Find every retry layer on the path: HTTP client defaults, SDK settings, queue redelivery, proxy or mesh retries and hand-written loops. Multiply the attempts: 3 layers of 3 attempts is 27 hits on the bottom service.
2. Keep retries in one layer, usually the one that knows whether the operation is safe to repeat, and turn the others off.
3. Classify failures. Retry connection errors, 429, 502, 503 and 504, and database serialization or deadlock errors (rerun the whole transaction). Do not retry other 4xx.
4. Treat a read timeout on a write as unknown outcome. Retry only if the operation is naturally idempotent or carries an idempotency key the server honours.
5. Use exponential backoff with full jitter: sleep a random time between 0 and `min(cap, base * 2^attempt)`.
6. Honour `Retry-After`; it may be seconds or an HTTP date.
7. Bound both attempts and total elapsed time, and keep the total inside the caller's own deadline.
8. Add a retry budget (for example, retries no more than about 10% of request volume) and count retries as a metric, separate from first attempts.
9. Test with a stub that fails N times, injecting the clock or sleep function so the test asserts delays without waiting.

## Watch out for
- Fixed delays make all clients retry together and recreate the spike.
- A retried request whose body is a consumed stream is sent empty or fails; buffer it or rebuild it per attempt.
- Logging only the final failure hides a dependency that succeeds on the third try all day.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Exactly one layer retries, the retryable set is written down, and a test shows both a bounded give-up and no retry on a non-retryable error.
