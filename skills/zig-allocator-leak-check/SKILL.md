---
name: zig-allocator-leak-check
version: 1.0.0
description: >
  Find leaks, double frees and use-after-free in Zig code using testing and debug allocators. Use when a Zig program grows in memory or crashes after freeing.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - zig
  - memory
  - testing
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: zig-allocator-leak-check
  official: true
  domain: tooling
  security_flags: []
---

# Zig Allocator Leak Check

## When to use
Zig code manages allocations manually and you need to prove ownership is correct.
## Steps
1. Run `zig version` first; the standard library and allocator names change between releases, so read the installed std source before writing code.
2. Run the code under tests using `std.testing.allocator`, which fails a test that leaks.
3. In programs, use the debug or general purpose allocator provided by that version and check the result of its deinit.
4. For each allocation, name the owner and place `defer` right after it when freed in scope, or `errdefer` when ownership passes to the caller on success.
5. Walk each error return in multi-step initializers; every earlier acquisition needs its own `errdefer`.
6. Use `std.testing.checkAllAllocationFailures` to inject out-of-memory at every allocation point.
7. Check containers holding allocated items: free the elements, and map keys you duplicated, before deinitializing the container.
8. Look for slices into a growable list kept across an append, which may reallocate and invalidate them.
9. With arenas, confirm nothing escapes past the arena's reset or deinit, and that long loops reset per iteration.
10. Document in each public function whether the caller owns the returned memory.
## Watch out for
- Returning a slice of a stack buffer is a dangling reference regardless of allocator.
- Release modes that remove safety checks can hide failures; test in Debug and ReleaseSafe.
- Swapping in an arena everywhere hides ownership and can grow without bound in servers.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Tests including allocation-failure injection pass with no leak reports, and ownership is stated for every returned allocation.
