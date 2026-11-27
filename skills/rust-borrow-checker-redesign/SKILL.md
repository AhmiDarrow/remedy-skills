---
name: rust-borrow-checker-redesign
version: 1.0.0
description: >
  Resolve stubborn Rust borrow and lifetime errors by changing data ownership instead of cloning blindly. Use when E0499, E0502, E0505 or E0597 keep returning after each patch.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - rust
  - refactoring
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: rust-borrow-checker-redesign
  official: true
  domain: backend
  security_flags: []
---

# Rust Borrow Checker Redesign

## When to use
Fixing one borrow error produces another, or lifetimes are spreading through many signatures.
## Steps
1. Run `cargo check`, take the first error, and read all labeled spans: where the borrow starts, the conflicting use, and where the first borrow is still needed later. `rustc --explain <code>` gives the rule.
2. Draw who owns each value and who needs it mutably, for how long.
3. If two fields of a struct are borrowed through a method taking `&mut self`, borrow the fields directly or split the struct so the method takes only what it uses.
4. If a loop mutates the collection it iterates, collect the needed changes first, iterate by index, or use `retain`, `iter_mut` or `split_at_mut`.
5. To move a value out from behind `&mut`, use `std::mem::take` or `replace`, or `Option::take`.
6. For map lookup then insert, use the entry API.
7. For graphs, parent links or observer lists, store items in a `Vec` or arena and refer to them by index or typed ID instead of references.
8. Avoid self-referential structs: store ranges or indices into the owned buffer.
9. Reach for `Rc<RefCell<T>>` or `Arc<Mutex<T>>` only when ownership is truly shared, and note that `RefCell` turns the compile error into a possible runtime panic.
## Watch out for
- A `clone` that silences the error may mean later writes go to a copy and are lost. Check that the original is not expected to change.
- Adding `'static` to satisfy a bound often forces leaking or cloning higher up.
- A lifetime parameter on a long-lived struct ties it to its source; owned fields are usually simpler.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
`cargo check` and tests pass, no clone was added without a stated reason, and the ownership of the contested value can be described in one sentence.
