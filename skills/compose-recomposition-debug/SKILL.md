---
name: compose-recomposition-debug
version: 1.0.0
description: >
  Find and fix excessive recomposition and scroll jank in Jetpack Compose using real measurements. Use when a Compose screen stutters or redraws far more than its data changes.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - android
  - performance
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: compose-recomposition-debug
  official: true
  domain: frontend
  security_flags: []
---

# Compose Recomposition Debug

## When to use
Lists drop frames, or typing in one field recomposes the whole screen.

## Steps
1. Measure in a release build with R8 enabled; debug builds are much slower and mislead. Use Macrobenchmark or a system trace for frames.
2. Use Layout Inspector recomposition and skip counts to find which composables run during the slow interaction.
3. For fast-changing values such as scroll offset or animation, defer the state read to the latest phase: pass a lambda, or use lambda modifiers such as `Modifier.offset { }` and `graphicsLayer { }`.
4. Wrap a value that changes less often than its inputs in `derivedStateOf` inside `remember`, for example whether the list has scrolled past the first item.
5. Give lazy list items stable `key`s and a `contentType`.
6. Check parameter stability with compiler reports. Prefer immutable data; interfaces such as `List` and classes from modules the Compose compiler does not process may be treated as unstable, depending on compiler version and skipping mode.
7. Move sorting, filtering, formatting and image decoding out of composition, into the view model or `remember` with correct keys.
8. Hoist reads downward so only the leaf that displays a value reads it.
9. Re-measure the same scenario.

## Watch out for
- `remember` without the right keys caches a stale result.
- Writing state that was already read earlier in the same composition causes a recomposition loop.
- Adding `@Stable` or `@Immutable` to a type that mutates silently produces screens that do not update.
- High recomposition counts that cost little are not worth contorting code for.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Frame timing for the same release-build interaction improves measurably, and the targeted composables no longer recompose when their displayed data is unchanged.
