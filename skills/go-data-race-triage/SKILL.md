---
name: go-data-race-triage
version: 1.0.0
description: >
  Use the Go race detector to find and correctly fix data races. Use when a test is intermittently wrong, a concurrent map write crashes, or -race prints a report.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - go
  - concurrency
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: go-data-race-triage
  official: true
  domain: testing
  security_flags: []
---

# Go Data Race Triage

## When to use
Shared state is touched from multiple goroutines and behavior is nondeterministic.
## Steps
1. Run `go test -race -count=20 ./...` and, for a service, run a race-built binary under realistic load. The detector only sees code paths that execute.
2. Read each report as three stacks: the access, the conflicting previous access, and where the goroutines were created. Find the single shared variable they have in common.
3. Check for a race-enabled build requirement: it needs cgo on most platforms.
4. Choose the fix by data shape. One counter or flag: types from `sync/atomic`. Several fields with an invariant: a `sync.Mutex` held across the whole read-modify-write. Ownership handoff: send on a channel and stop touching it. Read-mostly config: build a new value and swap with `atomic.Pointer`.
5. Check that methods on a type holding a mutex use pointer receivers; copying it copies the lock. `go vet` reports many such copies.
6. Do not return internal maps or slices from a locked getter; return a copy.
7. Check test code too: parallel subtests sharing fixtures and goroutines writing variables that the test reads without synchronization.
8. Rerun with high `-count` and `-cpu=1,4,8`, and add the race run to CI.
## Watch out for
- Adding `time.Sleep` changes timing and hides the report without fixing anything.
- Locking only the writer leaves the race; readers need the same lock.
- Making each access atomic still leaves check-then-act bugs, which the detector will not report.
- The race build uses much more memory and CPU, so do not benchmark with it.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Repeated race runs report nothing on the affected packages, and each fix names the variable and the synchronization that now orders its accesses.
