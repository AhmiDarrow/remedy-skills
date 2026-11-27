---
name: long-running-api-operations
version: 1.0.0
description: >
  Expose slow work through an accept-then-poll API with a status resource, cancellation and safe resubmission. Use when an endpoint takes longer than proxies or clients are willing to wait.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - api
  - async
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: long-running-api-operations
  official: true
  domain: backend
  security_flags: []
---

# Long Running Api Operations

## When to use
Report generation, imports, media processing or bulk changes keep hitting request timeouts, or users resubmit because nothing seems to happen.

## Steps
1. Validate everything cheap synchronously (auth, input shape, quota) so obvious errors still fail on the first request.
2. Persist an operation row before enqueuing: id, owner, type, input reference, state, progress, result reference, error, created and updated times, expiry.
3. Make creation and enqueue consistent, using an outbox or a sweeper that re-enqueues rows stuck in `queued`.
4. Respond `202 Accepted` with a `Location` header pointing at the status resource and a suggested `Retry-After`.
5. Use a small state machine: `queued`, `running`, `succeeded`, `failed`, `cancelled`. Update with a condition on the current state so a late worker cannot overwrite a terminal state.
6. Have the worker write a heartbeat; a reaper marks or requeues operations whose heartbeat is stale.
7. Accept an idempotency key so a resubmission returns the existing operation.
8. Make cancel a request the worker checks between safe units of work, and document what is already committed when it stops.
9. Check ownership on status, result and cancel alike. Give result links an expiry and purge old rows.

## Watch out for
- Percent progress invented from elapsed time stalls at 99%. Report counted units, or only the current stage.
- A status endpoint that returns 500 because the job failed confuses clients: the lookup succeeded, so return 200 with `state: failed`.
- Redelivered queue messages can run the job twice; claim the row atomically before working.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A test submits, polls to a terminal state, resubmits with the same key without a second run, and a killed worker leaves no operation stuck in `running`.
