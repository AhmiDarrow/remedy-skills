---
name: rate-limit-design
version: 1.0.1
description: >
  Design rate limits for login, public and expensive endpoints: keys, algorithm, shared counters, 429 responses and safe rollout. Use when protecting an API from abuse, brute force or runaway clients.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - security
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
  library_id: rate-limit-design
  official: true
  security_flags: []
---

# Rate Limit Design

## When to use
Endpoints can be hammered by attackers, bugs or one heavy customer.

## Steps
1. Name what each limit protects: password guessing, paid sends (email, SMS), costly queries or fair use. Look for existing gateway or middleware support first.
2. Measure real traffic per client and set limits above legitimate peaks, including shared office or carrier addresses and batch clients.
3. Choose keys per route: user or API key when authenticated, address when not. For login combine per-account, per-address and global limits so both one-account guessing and password spraying are slowed.
4. Take the client address only from forwarding headers set by your own trusted proxies. Consider grouping IPv6 by prefix.
5. Pick behaviour: token bucket for bursts with a steady rate, sliding window for strict counts, concurrency limits for slow expensive work. Weight costly operations.
6. With several instances, keep counters in a shared store with atomic increment and expiry. Decide per route what happens if the store is down: fail open for ordinary reads, stricter local fallback for login or paid actions.
7. Return 429 with `Retry-After` when known, in the API's normal error format. Do not reveal whether an account exists.
8. Prefer progressive delay or extra verification to hard account lockout, which lets an attacker lock others out.
9. Deploy in log-only mode, review who would be blocked, then enforce. Test boundary, reset, concurrent bursts, spoofed headers and multiple instances.

## Watch out for
- Fixed windows allow a double burst at the boundary.
- Limiting only the web login leaves reset, token and mobile endpoints open.
- Clients that retry immediately on 429 add load; document backoff.
- Application limits do not absorb volumetric network attacks.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each protected route has a documented key, limit and store-failure behaviour, and a test shows the limit holds under concurrent requests and cannot be bypassed with a forged address header.
