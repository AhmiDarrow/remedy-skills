---
name: react-server-state-cache
version: 1.0.0
description: >
  Replace hand-rolled fetch-in-effect code with a server-state cache, with sound query keys, staleness and invalidation. Use when lists show old data after edits or requests are duplicated.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - react
  - state
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: react-server-state-cache
  official: true
  domain: frontend
  security_flags: []
---

# React Server State Cache

## When to use
Components each fetch the same resource, loading flags are managed by hand, or a saved edit does not appear until reload.

## Steps
1. Check `package.json` for an installed data library (TanStack Query, SWR, RTK Query, a router with loaders). Use what is there and confirm its major version, since option names differ between majors.
2. List every read and the mutations that can change it. This table drives keys and invalidation.
3. Make one key factory per resource, hierarchical: all, list with filters, detail by id. Every variable the request uses (filters, page, locale, tenant) must be in the key.
4. Set staleness per resource from how fast it really changes. In TanStack Query the default stale time is zero, so mounting and window focus refetch; raise it for reference data.
5. Forward the abort signal the library passes into the request function so superseded requests are cancelled.
6. For each mutation, invalidate the narrowest key prefix that covers affected reads, or write the server's response into the detail entry and invalidate the lists.
7. Render four states distinctly: first load, error with no data, data with background refetch error, and empty result.
8. Clear the cache on logout or account switch.

## Watch out for
- A fetch wrapper that resolves on HTTP 4xx and 5xx makes the cache treat errors as data. Throw when `response.ok` is false.
- Copying query results into local state freezes them; read from the query and keep only the user's unsaved edits locally.
- A shared client instance created at module level during server rendering can leak one user's data into another's page.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
No component fetches that resource in its own effect, editing an item updates list and detail without reload, and the network panel shows one request per distinct key.
