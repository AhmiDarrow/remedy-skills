---
name: vue-reactivity-debug
version: 1.0.0
description: >
  Fix Vue 3 views that do not update or update too often because reactivity was lost or deep-watched. Use when a Vue value changes in code but not on screen, or watchers misfire.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - vue
  - debugging
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: vue-reactivity-debug
  official: true
  domain: frontend
  security_flags: []
---

# Vue Reactivity Debug

## When to use
Composition API code holds correct data in the console while the template shows old values, or a `watch` never fires or fires constantly.

## Steps
1. Check the installed Vue version in `package.json`; several behaviours below changed across 3.x minors.
2. Trace the value from source to template and find where it stops being reactive. `isRef`, `isReactive` and Vue DevTools help at each hop.
3. Look for destructuring of a `reactive` object or a Pinia store. Use `toRefs` or `toRef` for reactive objects and `storeToRefs` for store state; actions can be destructured directly.
4. Look for whole reassignment of a `reactive` variable, which replaces the proxy that others hold. Use a `ref` and assign `.value`, or mutate the existing object.
5. Props destructuring stays reactive only with the compiler support in newer 3.x releases; on older ones read `props.name` or use `toRefs(props)`.
6. For a watcher that never fires, pass a ref or a getter such as `() => props.id`, not the plain current value.
7. For a watcher that fires too much, replace `deep: true` with a getter returning only the fields that matter. Use `computed` for derived data instead of a watcher that writes state.
8. In async watchers, register cleanup with the watcher's cleanup callback to abort superseded requests.
9. Register watchers synchronously in `setup`; those created after an `await` in a composable may not stop with the component.

## Watch out for
- A `computed` with side effects runs at unpredictable times because it is lazy and cached.
- `shallowRef` ignores nested mutation; assign a new value or call `triggerRef`.
- Putting a large third-party instance (map, chart, editor) in deep reactive state can break it; use `shallowRef` or `markRaw`.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Changing the source value updates the template and fires the intended watcher exactly once, demonstrated in the running app or a component test.
