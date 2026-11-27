---
name: react-performance
version: 1.0.1
description: >
  Fix a slow React interaction by profiling it, finding why components render or take long, and re-measuring each change. Use when typing, clicking or updating a view feels laggy.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - react
  - perf
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: react-performance
  official: true
  security_flags: []
---

# React Performance

## When to use
A specific interaction in a React app is slow.

## Steps
1. Name the interaction, data size and device. Check the React version, the renderer and whether React Compiler is enabled, which changes how much manual memoisation helps.
2. Record it with the React DevTools Profiler, and the browser performance panel for time outside React (layout, parsing, network). Take timings from a production or profiling build; development is slower and Strict Mode double-invokes. If you cannot profile, ask the user to and send results.
3. For each slow commit, note which components rendered, why, and how long each took. A frequent cheap render may not matter.
4. Fix structure first: move state down to where it is used, pass expensive subtrees as `children`, split contexts or use selector subscriptions, and compute derived values during render instead of copying them into state with effects.
5. Cut expensive work: index lookups instead of nested searches, window long lists, defer heavy non-urgent updates with `useDeferredValue` or `startTransition`.
6. Memoise where the profile justifies it. `memo` only helps if props keep identity, so stabilise the specific objects and callbacks it receives.
7. Check list keys: stable ids. An index or random key causes wrong state or remounting. A component defined inside another remounts every render.
8. Change one thing, record again and compare, then check behaviour and tests.

## Watch out for
- Blanket `useMemo` and `useCallback` add complexity and stale-value bugs without a measured gain.
- A context provider whose value is a new object each render updates every consumer.
- Transitions reorder rendering priority but do not make slow work cheaper.
- A custom `memo` comparison that ignores function props leaves stale closures.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Before and after recordings of the same interaction show the improvement, the cause is stated, and behaviour is unchanged.
