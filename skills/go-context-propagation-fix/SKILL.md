---
name: go-context-propagation-fix
version: 1.0.0
description: >
  Thread context.Context correctly through Go code so cancellation and deadlines reach every blocking call. Use when cancelled requests keep working or jobs die with the request.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - go
  - reliability
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: go-context-propagation-fix
  official: true
  domain: backend
  security_flags: []
---

# Go Context Propagation Fix

## When to use
Client disconnects or timeouts do not stop downstream work, or work meant to outlive a request is cancelled with it.
## Steps
1. `grep` for `context.Background()` and `context.TODO()` outside `main`, initialization and tests. Each one inside a request path breaks the chain.
2. Add `ctx context.Context` as the first parameter along the chain from handler to the blocking call. Do not store it in a struct.
3. Switch to context-aware forms: `QueryContext`, `ExecContext`, `BeginTx`, `http.NewRequestWithContext`, `exec.CommandContext`, and dialers with `DialContext`.
4. In loops and channel operations, select on `ctx.Done()` and return `ctx.Err()`; for CPU loops, check periodically.
5. Place deadlines where the budget is known, and always `defer cancel()` right after creating one. Avoid a defer inside a long loop; move the iteration into a function.
6. For work that must continue after the response (audit write, async job), use `context.WithoutCancel` (Go 1.21+) plus its own timeout, and track it for shutdown.
7. Distinguish outcomes with `errors.Is(err, context.Canceled)` versus `context.DeadlineExceeded`, so client aborts are not counted as server failures.
8. Run `go vet ./...`, which catches lost cancel functions, then write a test that cancels mid-call and asserts a prompt return.
## Watch out for
- A shorter child deadline works, but a child cannot extend its parent's deadline.
- Context values are for request-scoped metadata with private key types, not for passing dependencies or optional parameters.
- A transaction begun with a context is rolled back when it is cancelled; do not reuse the request context for a commit that must happen.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The cancel test returns within a short bound, and no request path creates a fresh background context except the deliberately detached ones, each with a timeout.
