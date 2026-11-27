---
name: js-unhandled-promise-audit
version: 1.0.0
description: >
  Find floating, swallowed and incorrectly parallel promises in JavaScript or TypeScript. Use when errors vanish, Node exits on an unhandled rejection, or tests pass before work finishes.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - javascript
  - typescript
  - reliability
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: js-unhandled-promise-audit
  official: true
  domain: backend
  security_flags: []
---

# Js Unhandled Promise Audit

## When to use
Async failures are intermittent, silent, or crash the process far from their cause.
## Steps
1. In TypeScript, enable typed lint rules `@typescript-eslint/no-floating-promises` and `no-misused-promises`. They need type information configured; run lint and group the findings.
2. Run the app or tests with `node --trace-warnings --unhandled-rejections=strict` to get stacks for the ones that fire.
3. Search for `.forEach(async`. The loop does not wait; use `for...of` for sequential work or `await Promise.all(items.map(...))` for parallel.
4. Check `return somePromise` inside `try`: without `await`, the catch block never sees the rejection. Use `return await` there.
5. For promises created early and awaited later, an earlier rejection can be reported as unhandled. Attach all of them to one `Promise.all` or `allSettled` immediately.
6. Choose the combinator by intent: `all` fails fast but leaves other work running; `allSettled` reports every outcome; add a concurrency limit when the list is large.
7. Async event listeners and timer callbacks have no caller to catch errors. Wrap each body in try/catch.
8. Look at every empty `.catch()`; either handle a named expected error and rethrow the rest, or let it propagate.
9. Add one test per fixed path that makes the dependency reject and asserts the error surfaces.
## Watch out for
- A global `unhandledRejection` handler that only logs keeps a process running in an unknown state. Log, flush, and exit.
- Prefixing a call with `void` satisfies the linter without handling anything.
- Rejecting `Promise.all` does not cancel siblings; pass an `AbortSignal` if they must stop.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Lint reports no floating or misused promises (or each exception has a written reason), and the injected-rejection tests pass.
