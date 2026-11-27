---
name: go-goroutine-leak-hunt
version: 1.0.0
description: >
  Find goroutines that never exit in a Go service and fix their lifecycle. Use when goroutine count or memory climbs steadily and does not fall after traffic stops.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - go
  - concurrency
  - debugging
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: go-goroutine-leak-hunt
  official: true
  domain: backend
  security_flags: []
---

# Go Goroutine Leak Hunt

## When to use
`runtime.NumGoroutine()` or the metrics for it grows with uptime.
## Steps
1. Confirm it is a leak: record the count at idle, apply load, stop, wait past all timeouts, record again.
2. Get stacks from the pprof endpoint `/debug/pprof/goroutine?debug=1`, which groups identical stacks with counts, or `debug=2` for each one's wait time. Keep this endpoint on a private interface.
3. Take two profiles minutes apart and look for the stack whose count grew.
4. Classify the blocked line. Channel send with no receiver: the receiver returned early, so buffer the channel for the number of senders or select on `ctx.Done()`. Channel receive or `range`: nobody closes it; the sole sender should close.
5. Network or database waits: set client timeouts and use context-aware calls. The zero-value HTTP client has no timeout.
6. Check HTTP response bodies are closed on every path that got a non-nil response.
7. Check tickers and background loops have a stop path and that `context.WithCancel` or `WithTimeout` cancel functions are called.
8. Give each goroutine an owner that can signal stop and wait for exit, using a `sync.WaitGroup` or an errgroup.
9. Add a test that runs the operation repeatedly, including the error and cancel paths, and asserts the count returns to baseline with a bounded retry, or use a goroutine leak checking library if present.
## Watch out for
- Closing a channel from the receiver side or from multiple senders panics.
- Comparing counts immediately after cancel gives false positives; exiting takes a moment.
- Idle keep-alive connections own goroutines; that is expected until the idle timeout.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
After the load test and timeouts, the goroutine count returns to its idle baseline, and the regression test covers the path that leaked.
