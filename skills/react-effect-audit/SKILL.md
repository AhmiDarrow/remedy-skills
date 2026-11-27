---
name: react-effect-audit
version: 1.0.0
description: >
  Remove or repair misused React useEffect calls that cause double renders, request races and sync loops. Use when a component has chains of effects or misbehaves under Strict Mode.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - react
  - hooks
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: react-effect-audit
  official: true
  domain: frontend
  security_flags: []
---

# React Effect Audit

## When to use
A component renders stale values for one frame, effects set state that triggers other effects, or something fires twice in development.

## Steps
1. `grep` for `useEffect(` and `useLayoutEffect(` in the affected tree. For each, write one line: which external system does it synchronise with? Network, DOM API, subscription, timer and third-party widget count. Props and state do not.
2. Effect that computes state from props or state: delete the state and compute during render. Use `useMemo` only if the computation is measurably slow.
3. Effect that reacts to a user action (post, toast, navigate after a flag flips): move the code into the event handler and delete the flag.
4. Effect that resets state when an id changes: pass that id as `key` to the component so it remounts with fresh state.
5. Effect that subscribes to an external store: use `useSyncExternalStore`.
6. For effects that remain, return a cleanup that reverses setup exactly: `removeEventListener` with the same function reference, `clearInterval`, `AbortController.abort()` for fetches.
7. Run the linter with the `react-hooks/exhaustive-deps` rule. Fix a dependency warning by moving objects or functions inside the effect, not by disabling the line.
8. Run in Strict Mode and confirm mount, unmount, mount leaves one subscription and one visible result.

## Watch out for
- Guarding with a `didRun` ref to silence the development double call hides a missing cleanup that will still break on real remounts.
- An object or array literal created during render and listed as a dependency re-runs the effect every render.
- Removing an effect can change ordering that a parent relied on through an `onChange` callback; check each caller of such callbacks.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every remaining effect names an external system and has matching cleanup, the dependency lint passes without suppressions, and the reported symptom no longer reproduces in Strict Mode.
