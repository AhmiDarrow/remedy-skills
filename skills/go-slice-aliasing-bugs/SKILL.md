---
name: go-slice-aliasing-bugs
version: 1.0.0
description: >
  Debug Go bugs caused by slices sharing backing arrays through append, subslicing and reuse of buffers. Use when data changes unexpectedly after an unrelated append.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - go
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
  library_id: go-slice-aliasing-bugs
  official: true
  domain: backend
  security_flags: []
---

# Go Slice Aliasing Bugs

## When to use
Elements get overwritten, stored results all look like the last one, or small slices keep huge buffers alive.
## Steps
1. Print `len`, `cap` and `&s[0]` for the two slices that seem linked. Equal or overlapping addresses confirm shared storage.
2. Find the creation point. `b := a[:n]` shares memory, and `append(b, x)` overwrites `a[n]` whenever capacity allows.
3. Where the callee must not touch the caller's tail, use a full slice expression `a[low:high:high]` to force a copy on the next append.
4. Where independence is needed, copy: `slices.Clone` (Go 1.21+) or `append([]T(nil), s...)`.
5. Audit retained data from reused buffers: `bufio.Scanner.Bytes()` and many read loops return memory that is overwritten on the next iteration. Copy before storing.
6. Check functions that append to a parameter without returning it; the caller's length does not change, but its backing array may.
7. For in-place filtering such as `out := s[:0]`, confirm no one else still uses `s`, and clear the leftover tail if it holds pointers.
8. For memory retention, clone small pieces cut from large byte slices or strings (`bytes.Clone`, `strings.Clone`).
9. Write a regression test that mutates one result and asserts the other is unchanged, using a starting slice with spare capacity.
## Watch out for
- Tests with literal slices have no spare capacity, so append reallocates and the bug does not reproduce.
- `slices.Clone` is shallow; pointer, map and slice elements are still shared.
- Pooled buffers from `sync.Pool` must not be referenced after being put back.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The regression test fails on the old code and passes on the new, and every escaping slice from a reused buffer is copied.
