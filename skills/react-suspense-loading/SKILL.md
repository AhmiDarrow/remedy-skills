---
name: react-suspense-loading
version: 1.0.0
description: >
  Arrange Suspense boundaries and data preloading to avoid spinner cascades, layout jumps and content flashing away. Use when a page loads in staggered spinners or blanks on navigation.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - react
  - loading
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.snapshot
metadata:
  source: library
  library_id: react-suspense-loading
  official: true
  domain: frontend
  security_flags: []
---

# React Suspense Loading

## When to use
Nested components each show their own spinner, requests start one after another, or changing a filter replaces visible results with a fallback.

## Steps
1. Record the network waterfall on a throttled connection. Mark requests that wait for a component to render although their inputs were already known.
2. Start those requests at the route level (loader, preload call or server component) and let children read the pending result. Suspense displays waiting; it does not by itself remove waterfalls.
3. Confirm the data source supports Suspense. A plain fetch inside `useEffect` never triggers a fallback.
4. Group boundaries by what the user should see together: shell immediately, primary content as one block, slow secondary panels separately.
5. Give each fallback the final block's dimensions so nothing shifts on arrival.
6. For updates to already visible content (tabs, filters, pagination), wrap the state change in `startTransition` so old content stays while the new loads, and show a pending hint using `isPending` from `useTransition`.
7. Where a switch should show a fallback because the subject changed entirely, key the boundary by the subject id.
8. Pair each boundary with an error boundary, since a rejected resource goes there.

## Watch out for
- Creating a new promise during render and reading it with `use` suspends forever or refetches; the promise must be cached outside the render.
- Keeping the controlled input's value inside a transition makes typing lag; update the input urgently and defer only the results.
- Many tiny boundaries produce a popcorn effect that feels slower than one well-sized block.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
On a throttled connection the shell appears first, independent requests overlap in the waterfall, and changing filters never blanks content that was already shown.
