---
name: server-client-component-split
version: 1.0.0
description: >
  Place the boundary between server and client components so less JavaScript ships and no server-only code leaks. Use when adopting server components or when a client directive has spread up the tree.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - react
  - architecture
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: server-client-component-split
  official: true
  domain: frontend
  security_flags: []
---

# Server Client Component Split

## When to use
A framework with React Server Components has `'use client'` on whole pages or layouts, builds fail on passing functions across the boundary, or secrets risk reaching the bundle.

## Steps
1. Record the current client JavaScript per route from the production build output, as the baseline.
2. `grep` for `'use client'`. For each file, list what truly needs the client: state, effects, event handlers, browser APIs, or a library that uses them. Remember that everything it imports joins the client bundle.
3. Push the directive down to the smallest interactive leaf, such as the like button rather than the article page.
4. Where a client wrapper must surround server content (tabs, drawer, provider), pass that content as `children` from a server parent instead of importing it inside the client file.
5. Check props crossing the boundary: they must be serialisable. Plain functions and class instances are not; server functions marked `'use server'` are the exception.
6. Pass only the fields the client renders. A whole database record sent as a prop is visible in the page payload.
7. Mark modules holding secrets or database access with the `server-only` package or the framework's equivalent so a bad import fails the build.
8. Treat every server function as a public endpoint: authenticate, authorise and validate its arguments inside it.
9. Rebuild and compare route sizes.

## Watch out for
- A barrel file that re-exports both kinds of module can drag server code into client imports or the reverse.
- Third-party providers often need a small client wrapper file; do not convert the root layout for one.
- Moving fetches into nested server components can create sequential waterfalls; start independent requests together.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The build passes, client JavaScript for the changed routes is no larger and ideally smaller than the baseline, and the page payload contains no unused sensitive fields.
