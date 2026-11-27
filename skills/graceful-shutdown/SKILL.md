---
name: graceful-shutdown
version: 1.0.1
description: >
  Make servers and workers stop cleanly on termination signals, draining in-flight work within a deadline. Use when deploys cause dropped requests, duplicate jobs or processes that get force-killed.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - reliability
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
  library_id: graceful-shutdown
  official: true
  security_flags: []
---

# Graceful Shutdown

## When to use
A long-running process is restarted or scaled and work must not be lost or corrupted.

## Steps
1. Find how it is stopped: signal sent, grace period and kill signal for the orchestrator, service manager or container runtime. Windows services and consoles use different events from Unix signals.
2. Confirm the signal reaches the process. Shell-form container commands and package script runners may not forward it; a process running as PID 1 gets no default signal action.
3. List in-flight work: requests, streams and sockets, queue messages, scheduled tasks, background threads and buffered logs or telemetry.
4. In the handler, only start the shutdown sequence, and make it safe to trigger twice.
5. Mark the instance not ready and stop accepting new work. Where load balancers learn of removal asynchronously, keep serving for a short measured delay before closing the listener.
6. Drain with the framework's shutdown method. Close idle keep-alive connections, tell long-lived streams to reconnect, and cancel what cannot finish.
7. Consumers stop fetching, then finish and acknowledge or return each held message. Checkpoint long jobs so they can resume.
8. After workers finish, flush telemetry and close pools and clients in reverse dependency order.
9. Set an internal deadline shorter than the external grace period, counting any pre-stop delay; log what was abandoned and exit.
10. In a test environment, test under load: send the real stop signal during slow requests and jobs, then check for errors, lost or repeated work and exit time.

## Watch out for
- Closing the database pool while requests are still using it.
- In some runtimes, adding a signal listener removes the default exit, so the process hangs unless it exits or all handles close.
- One drain step with no timeout consuming the whole grace period.
- Assuming shutdown always runs; crashes and forced kills still require recoverable work.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A stop during load completes within the grace period with no unexpected request failures or lost jobs, and the forced-timeout path has been exercised.
