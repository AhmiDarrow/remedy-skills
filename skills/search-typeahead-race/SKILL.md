---
name: search-typeahead-race
version: 1.0.0
description: >
  Fix search-as-you-type so stale responses never replace newer ones, with debouncing, cancellation and IME safety. Use when suggestions flicker or show results for an earlier query.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - forms
  - async
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: search-typeahead-race
  official: true
  domain: frontend
  security_flags: []
---

# Search Typeahead Race

## When to use
Fast typing shows results for a shorter prefix, every keystroke hits the server, or Asian-language input triggers searches mid-composition.

## Steps
1. Reproduce with throttling or a server stub that delays short queries longer than long ones.
2. Keep the input value updating immediately; debounce only the query used for fetching, typically 150 to 300 ms.
3. Abort the previous request with `AbortController`, and also check that a response's query still matches the current one before applying it.
4. Treat aborts as normal, not as errors to display.
5. Do not search during composition: track `compositionstart` and `compositionend`, and ignore Enter while `event.isComposing` is true.
6. Normalise the cache key (trim, and case if the server ignores it) and reuse cached results when the user deletes characters.
7. Set rules for empty and very short queries, remembering that some languages use meaningful single characters.
8. While loading, keep previous results visibly marked as updating; show No results only after the current query completes empty.
9. Announce result counts politely for screen readers, after typing settles.

## Watch out for
- Debounce alone does not fix ordering; two requests can still be in flight.
- A loading flag cleared by an old request's `finally` hides the spinner while the new one runs.
- Rendering matched text with injected HTML for highlighting opens script injection; split strings into elements instead.
- Pre-selecting the first suggestion can make Enter submit something the user did not type.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Under inverted response delays the list always matches the text in the box, rapid typing yields only a few requests, and IME composition triggers no search or accidental selection.
