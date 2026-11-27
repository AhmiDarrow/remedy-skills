---
name: go-heap-profile-allocation
version: 1.0.0
description: >
  Use Go heap and allocation profiles to reduce memory use or GC cost. Use when a Go service has high RSS, frequent garbage collection or gets OOM killed.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - go
  - profiling
  - performance
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
metadata:
  source: library
  library_id: go-heap-profile-allocation
  official: true
  domain: backend
  security_flags: []
---

# Go Heap Profile Allocation

## When to use
Memory is the constraint and you need to know which call sites are responsible.
## Steps
1. Decide the question. Live memory is `inuse_space`; GC pressure is `alloc_space` or `alloc_objects`. They often point to different code.
2. Fetch `/debug/pprof/heap` at the high-memory moment, or use `go test -bench . -benchmem -memprofile mem.out`.
3. Open with `go tool pprof -sample_index=inuse_space <file>`, then use `top`, `list <func>` and `peek`.
4. For growth over time, compare two snapshots with `-diff_base`.
5. Compare heap size with process RSS. A large gap suggests goroutine stacks, cgo or memory-mapped data, or freed memory not yet returned; read `runtime/metrics` before blaming the heap.
6. Run with `GODEBUG=gctrace=1` to see collection frequency and heap goals.
7. Reduce allocations at the top sites: preallocate with known capacity, stream instead of reading whole bodies, avoid repeated string and byte conversions in hot loops, and use `go build -gcflags=-m` to see why a value escapes.
8. For container limits, set `GOMEMLIMIT` somewhat below the limit to leave headroom for non-heap memory; tune `GOGC` only after measuring.
9. Verify with benchmarks compared by `benchstat` over several runs.
## Watch out for
- The heap profile is sampled and reflects the most recently completed collection; add `?gc=1` for a fresh one.
- `sync.Pool` added without evidence adds complexity and can retain oversized buffers.
- `GOMEMLIMIT` is a soft limit; when live data exceeds it, the collector burns CPU without preventing an OOM.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The top allocation or retention site is identified from a profile, and a second profile under the same workload shows the measured reduction.
