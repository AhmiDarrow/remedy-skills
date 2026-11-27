---
name: swiftui-state-ownership
version: 1.0.0
description: >
  Choose correct SwiftUI state ownership with State, Binding and Observable so data neither resets nor goes stale. Use when views lose input, objects are recreated or updates do not appear.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - ios
  - swiftui
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: swiftui-state-ownership
  official: true
  domain: frontend
  security_flags: []
---

# Swiftui State Ownership

## When to use
A view model reinitialises on parent updates, edits do not propagate, or a codebase is moving to Observation.

## Steps
1. Check the deployment target. The `@Observable` macro needs iOS 17 or matching releases; older targets use `ObservableObject`.
2. For each piece of data name the single owner and its intended lifetime.
3. With Observation: the owning view stores the object in `@State`; children receive it as a plain property; use `@Bindable` where bindings are needed; share widely through `.environment(object)` and `@Environment(Type.self)`.
4. With `ObservableObject`: the creator uses `@StateObject`, recipients use `@ObservedObject`, shared uses `@EnvironmentObject`.
5. For value types use `@State` privately in the owner and `@Binding` where a child edits it.
6. When state resets or persists wrongly, inspect view identity: changing `.id()`, `if` branches that swap structurally different views, and unstable `ForEach` ids.
7. Replace `onAppear` loading with `.task(id:)` so work cancels on disappearance and restarts when the input changes.
8. Keep UI-bound model mutation on the main actor.
9. Verify by navigating away and back, rotating and updating the parent while editing.

## Watch out for
- `@State var x` initialised from an initializer parameter takes only the first value; later parent changes are ignored.
- An object created inline in `@ObservedObject` is rebuilt whenever the view struct is.
- The expression initialising `@State` with an observable object may be evaluated again even though SwiftUI keeps the first instance, so initializers must be free of side effects.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each model has one owner, the reported reset or stale case is gone on a device or simulator, and loading runs once per distinct input.
