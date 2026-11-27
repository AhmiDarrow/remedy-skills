---
name: api-contract-review
version: 1.0.1
description: >
  Review HTTP API endpoints for input validation, object-level authorization, status codes, retries, pagination and error shape. Use when reviewing a new or changed route before it ships.
author: Remedy Official
license: Apache-2.0
tags:
  - api
  - backend
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
metadata:
  source: library
  library_id: api-contract-review
  official: true
  security_flags: []
---

# Api Contract Review

## When to use
A pull request or design adds or changes endpoints that other code will depend on.

## Steps
1. List each changed route with method, who may call it, and what it reads or writes. Read the handler, its middleware and a neighbouring established endpoint to learn house conventions.
2. Authorization: for every identifier in path, query or body, find the line that checks this caller may touch that object. Being logged in is not enough. Check list filters and nested resources too.
3. Input: schema validation at the boundary, bounds on strings, numbers, arrays and body size. Writable fields must be an allowlist so a client cannot set `role`, `owner_id` or price.
4. Output: serialize named fields, not whole database rows. Look for secrets, internal ids and other users' data.
5. Status and errors: 401 versus 403, whether 404 should hide existence, 409 for state conflicts, 422 or 400 as the codebase does it. One stable error shape with a machine code; no stack traces or SQL text.
6. Safety on repeat: GET changes nothing; say what a retried POST does; check for lost updates on concurrent writes (version field or `If-Match`).
7. Lists have a server-enforced maximum and stable order. Expensive or credential routes have rate limits.
8. Compare with the previous contract for removed fields, new required inputs and changed types, and check the description file and tests cover the denied cases.
9. Report findings by severity with file and line, a concrete failing request, and the fix.

## Watch out for
- Authorization applied to read routes but forgotten on update, delete, export or bulk variants.
- Trusting a tenant or user id supplied in the body.
- Style preferences listed alongside security holes with equal weight.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every changed route has its authorization check identified or reported missing, and each finding names a location, an example request and a fix.
