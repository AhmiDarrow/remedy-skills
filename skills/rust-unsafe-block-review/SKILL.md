---
name: rust-unsafe-block-review
version: 1.0.0
description: >
  Review Rust unsafe code for soundness by writing down each invariant and testing it. Use when adding or auditing unsafe blocks, FFI bindings or manual Send and Sync impls.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - rust
  - review
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - edit
metadata:
  source: library
  library_id: rust-unsafe-block-review
  official: true
  domain: security
  security_flags: []
---

# Rust Unsafe Block Review

## When to use
A change introduces or modifies `unsafe`, or a crash appears in code near it.
## Steps
1. List every `unsafe` block, function, impl and extern block with `grep`. Include safe functions whose correctness an unsafe block relies on.
2. For each operation, read the called function's Safety section and write a `// SAFETY:` comment answering every condition with a concrete reason.
3. Check pointers for non-null, alignment, initialization, bounds of the same allocation, and lifetime. Check no `&mut` exists alongside any other live reference to the same data.
4. Replace `mem::uninitialized` or zeroing of arbitrary types with `MaybeUninit`; a value with invalid bits (a `bool` of 2, a null reference) is undefined behavior immediately.
5. Check panic paths: if user code can panic mid-way, drop must not see half-initialized data or double free.
6. For FFI, verify `#[repr(C)]` layouts, integer widths, string NUL termination, who frees each allocation with which allocator, and that panics do not unwind across a boundary not declared to allow it.
7. For `unsafe impl Send` or `Sync`, explain what synchronizes access, and check generic bounds are not too loose.
8. Test with `cargo +nightly miri test` for pure Rust paths; Miri cannot run most foreign calls, so use address sanitizer there.
9. Make the public safe API impossible to misuse: no safe caller may trigger undefined behavior with any input.
## Watch out for
- Passing tests do not show soundness; undefined behavior often works until an optimizer change.
- `CString::new(s).unwrap().as_ptr()` leaves a dangling pointer once the temporary is dropped.
- `from_raw_parts` needs a non-null aligned pointer even for length zero.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every unsafe site has a SAFETY comment matching its documented conditions, and Miri or a sanitizer runs cleanly over the covered paths.
