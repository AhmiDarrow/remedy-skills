---
name: health-endpoints
version: 1.0.1
description: >
  Design liveness, readiness and startup health checks that restart or remove instances only when that helps. Use when adding health endpoints or when probes cause restart loops or outages.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - ops
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
  library_id: health-endpoints
  official: true
  security_flags: []
---

# Health Endpoints

## When to use
An orchestrator, load balancer or monitor needs to know the state of a service.

## Steps
1. Find who consumes each check and what it does on failure: restart, stop routing, replace the machine or page someone. One endpoint serving several consumers may not be safe.
2. Liveness answers whether restarting this process would help. Keep it cheap, with no database or network dependency, but able to fail when the serving loop is stuck.
3. Readiness answers whether this instance should get traffic now: initialisation done, required local resources usable, not draining.
4. Decide each dependency separately. If a shared dependency fails, every instance can become unready at once; where the service can still return cached data or a useful error, report degraded state elsewhere instead.
5. Use a startup check or equivalent for slow initialisation rather than a very long liveness delay.
6. Make dependency checks use short timeouts and a cached or background result, so probes cannot overload a struggling dependency.
7. Return a success status when healthy and 503 when not. Keep public bodies minimal; put detail behind authentication or logs. Exempt probes from login and avoid flooding access logs.
8. Set period, timeout and failure threshold from measured startup and pause times. Run the check through the same port and middleware that matter to real serving, and document any separate management port.
9. Outside production, test: slow start, blocked worker, dependency outage, recovery and shutdown. Observe both responses and orchestrator actions.

## Watch out for
- A database outage failing liveness and restarting the whole fleet, followed by a reconnect storm.
- A health route answering from a separate thread while all request workers are stuck.
- Checks that write data or call a paid third-party API.
- Treating a healthy probe as proof that users succeed; keep monitoring user-facing errors.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each check has a documented meaning and consumer, failure tests produce the intended restart or routing action, and probe settings are recorded with the deployment config.
