---
name: angular-signals-migration
version: 1.0.0
description: >
  Move Angular components from manual subscriptions and decorator inputs to signals incrementally and safely. Use when modernising change detection or removing subscription boilerplate in Angular.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - angular
  - migration
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - todo
metadata:
  source: library
  library_id: angular-signals-migration
  official: true
  domain: frontend
  security_flags: []
---

# Angular Signals Migration

## When to use
Components juggle `subscribe` calls, `ngOnChanges` and manual `markForCheck`, and the team wants signal-based state.

## Steps
1. Read `package.json` for the Angular version. Signal inputs, queries and related APIs reached stable status in different releases, so check that version's documentation before using each.
2. List per component: local mutable fields, values derived in getters or `ngOnChanges`, and every subscription with its teardown.
3. Convert local state to `signal` and derivations to `computed`. Update with `set` or `update` and create new arrays and objects rather than mutating in place.
4. Convert inputs and outputs to `input()` and `output()`, using the CLI migration schematics where the version provides them, and review the result.
5. Keep RxJS for event streams with time (debounce, retry, websockets). Bridge at the edge with `toSignal` and `toObservable` from `@angular/core/rxjs-interop`.
6. Give `toSignal` an `initialValue` where the source is not synchronous, or handle `undefined` in the template.
7. Remaining manual subscriptions get `takeUntilDestroyed`.
8. Use `effect` only to push values out to non-signal code such as storage or a chart library.
9. Switch to `OnPush` after a component's template reads only signals, inputs and async pipes, then test it.

## Watch out for
- Mutating an array held in a signal keeps the same reference, so dependents are not notified.
- `toSignal` needs an injection context; calling it inside a method throws.
- An effect that copies one signal into another creates ordering bugs that `computed` or a linked signal avoids.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Converted components build and pass tests, contain no unmanaged subscriptions, and update correctly on screen with `OnPush` enabled.
