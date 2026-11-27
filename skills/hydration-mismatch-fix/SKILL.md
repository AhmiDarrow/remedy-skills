---
name: hydration-mismatch-fix
version: 1.0.0
description: >
  Track down server and client render differences that cause hydration errors, flicker or lost event handlers. Use when a server-rendered page logs hydration warnings or re-renders from scratch.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - ssr
  - debugging
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - computer.navigate
  - computer.snapshot
metadata:
  source: library
  library_id: hydration-mismatch-fix
  official: true
  domain: frontend
  security_flags: []
---

# Hydration Mismatch Fix

## When to use
The console reports hydration failed or text content mismatch, or a server-rendered page visibly jumps as the client takes over.

## Steps
1. Reproduce in a development build, which names the mismatching element. Try a clean browser profile first: extensions that inject attributes or nodes cause false reports.
2. Compare the server HTML (view source or `curl`) with the first client render at the reported node.
3. Search that path for values that differ per environment: `Date.now()`, `new Date()` formatting, `Math.random()`, `toLocaleString` without explicit locale and time zone, `window`, `localStorage`, `matchMedia`, user agent checks.
4. Check HTML validity. A `div` inside `p`, nested anchors, or a `tr` outside `tbody` makes the browser rewrite the tree before the framework sees it.
5. Fix by making inputs identical: serialise the server's value into the payload, fix locale and time zone, and generate ids with `useId` or the framework equivalent.
6. For values only the browser knows, render a same-sized placeholder first and set the real value after mount, or disable server rendering for that one component.
7. For theme, apply the class with a small inline script in `head` before paint, or store the choice in a cookie the server can read.
8. Verify in a production build with a non-default locale and time zone.

## Watch out for
- `suppressHydrationWarning` applies only one level deep and only hides the report; reserve it for single text or attributes such as a timestamp.
- `typeof window !== 'undefined'` inside render creates exactly the two different outputs you are trying to remove.
- A CDN or proxy that minifies HTML can alter markup in production only.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A production load with a different time zone and saved preferences shows no hydration errors and no visible jump at the repaired component.
