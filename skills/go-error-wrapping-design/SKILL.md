---
name: go-error-wrapping-design
version: 1.0.0
description: >
  Make Go errors inspectable and informative with wrapping, sentinel and typed errors. Use when callers compare error strings, context is missing from logs, or a nil error is not nil.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - go
  - error-handling
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: go-error-wrapping-design
  official: true
  domain: backend
  security_flags: []
---

# Go Error Wrapping Design

## When to use
Debugging production failures is hard because errors lack context, or control flow depends on message text.
## Steps
1. `grep` for `.Error() ==`, `strings.Contains(err` and `err == ` comparisons. These break once anything wraps the error.
2. Decide what callers need to branch on. No branching: wrap with context only. One condition: an exported sentinel `var ErrNotFound = errors.New(...)`. Data needed: a struct type with fields.
3. Wrap with `fmt.Errorf("load user %d: %w", id, err)`. Describe the operation attempted; skip "failed to" at every level, which produces repetitive chains.
4. Use `%w` only when the underlying error is part of your public contract. Use `%v` to hide an implementation detail such as a specific driver error.
5. Replace comparisons with `errors.Is` and type assertions with `errors.As`.
6. Translate storage or transport errors into domain errors at the package boundary, and map domain errors to status codes in one place.
7. Check the typed-nil trap: a function returning `error` must return literal `nil`, never a nil pointer of a custom error type, because the interface would be non-nil.
8. Log each error once, at the layer that handles it. Return it everywhere else.
9. Check deferred `Close` on writers and propagate its error through a named return without overwriting an earlier one.
## Watch out for
- Switching `%v` to `%w` or back changes API behavior for callers using `errors.Is`.
- Shadowing `err` with `:=` inside a block can silently drop an assignment; read each block carefully.
- Messages that embed tokens, queries with values or personal data end up in logs.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
No branching depends on error text, tests assert the important conditions with `errors.Is` or `errors.As`, and a sample failure log reads as a single clear chain.
