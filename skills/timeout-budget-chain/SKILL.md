---
name: timeout-budget-chain
version: 1.0.0
description: >
  Set connect, read and overall deadlines along a request path so inner calls give up before their callers do. Use when requests hang, pile up, or time out at the edge while work continues behind.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - reliability
  - performance
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: timeout-budget-chain
  official: true
  domain: backend
  security_flags: []
---

# Timeout Budget Chain

## When to use
A slow dependency exhausts workers or connections, or users see gateway timeouts while the backend later logs success.

## Steps
1. Draw the real chain: client, load balancer or proxy, app server, handler, each outbound call, database. For each hop record the configured timeout and where it is set. Mark "library default" and look the default up for the installed version; some clients wait forever.
2. Pick the user-facing deadline first, then give each inner hop less than what remains above it, with room to build an error response.
3. Separate connect timeout (short, since a healthy network connects fast) from read or response timeout (sized from the observed p99 plus margin).
4. Check what the read timeout means. In many clients it limits the gap between bytes, so a trickling response never trips it; add a total deadline too.
5. Propagate the remaining deadline downstream (gRPC deadlines, a context or cancellation token, or an agreed header) so later calls do not start work nobody will wait for.
6. Bound database time with `statement_timeout` and `lock_timeout` in PostgreSQL, or the equivalent, set per role or transaction.
7. Add timeouts for waiting on a pool connection; it is often the missing one.
8. Prove it with a stub that accepts the connection and never answers, and another that sends one byte every few seconds.

## Watch out for
- Giving up on the client does not cancel server work unless cancellation is wired through; the query may keep running.
- Retries must fit inside the same budget: three 5 s attempts do not fit a 10 s deadline.
- A global statement timeout also kills migrations and reports; give those their own setting.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every hop has an explicit timeout in a written table, each inner value fits within its caller's, and the hanging-stub test fails fast.
