---
name: svelte-runes-migration
version: 1.0.0
description: >
  Migrate a Svelte codebase from legacy reactive statements and export let to runes without changing behaviour. Use when upgrading components to Svelte 5 syntax.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - svelte
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
  library_id: svelte-runes-migration
  official: true
  domain: frontend
  security_flags: []
---

# Svelte Runes Migration

## When to use
A project on Svelte 5 still uses `export let`, `$:` statements, slots and event dispatchers, and wants runes mode.

## Steps
1. Confirm the installed Svelte version is 5 or later and that UI libraries support it. Run the existing tests and note the baseline.
2. Run the official migrator (`npx sv migrate svelte-5`) on a clean branch, then review the diff by hand. Treat its output as a draft.
3. Classify every former `$:` statement. A computed value becomes `$derived` (or `$derived.by` for a block). A side effect becomes `$effect`. An effect that only assigns state is a derived value in disguise.
4. Check props: `export let` becomes destructuring from `$props()`. Props the child writes back to need `$bindable()` and `bind:` at the parent.
5. Replace `createEventDispatcher` with callback props and update every parent in the same change, since a missed listener fails silently.
6. Replace slots with snippets and `{@render}`; the default slot becomes the `children` prop.
7. Move shared state into `.svelte.js` or `.svelte.ts` modules where runes are allowed. Export an object or accessor functions, not a reassigned `$state` variable.
8. Convert leaf components first, run the compiler and tests after each batch, and click through forms and lists.

## Watch out for
- `$effect` tracks only what it reads synchronously; values read after an `await` or inside a timeout are not dependencies.
- `$:` statements ran before the DOM update, effects run after it. Use `$effect.pre` where DOM measurement depended on the old order.
- `$state` objects are deep proxies; APIs that require plain objects may need `$state.snapshot`.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
No legacy syntax remains in the converted folders, the build has no migration warnings there, tests match the baseline, and every former dispatched event has a verified callback.
