---
name: http-cache-headers
version: 1.0.0
description: >
  Choose Cache-Control, validators and Vary for each class of response so caches speed things up without serving stale or private data. Use when setting up or debugging HTTP or CDN caching.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - http
  - caching
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: http-cache-headers
  official: true
  domain: backend
  security_flags: []
---

# Http Cache Headers

## When to use
Responses are re-fetched needlessly, users see old content after a deploy, or a shared cache may be storing personal responses.

## Steps
1. Sample real responses with `curl -sI` (and a GET with `-D -` where HEAD differs) for each class: hashed assets, HTML, public API data, authenticated data, errors.
2. Content-hashed assets: `public, max-age=31536000, immutable`.
3. HTML that references them: `no-cache`, which allows storing but requires revalidation. `no-store` forbids storing at all; keep it for sensitive responses.
4. Personalized responses: `private` or `no-store`. Check that framework or CDN defaults do not add `public`.
5. Shared caching of public data: use `s-maxage` for the shared cache and a shorter `max-age` for browsers; consider `stale-while-revalidate` where brief staleness is acceptable.
6. Add `ETag` or `Last-Modified` and confirm a conditional request returns 304.
7. Set `Vary` for every request header that changes the body, such as `Accept-Encoding`, `Accept-Language` or `Origin` with dynamic CORS. Check the CDN's actual cache key, since some ignore parts of `Vary`.
8. Request twice and read `Age` and the cache-status header to confirm hit or miss; repeat with two different test users.

## Watch out for
- With no `Cache-Control`, caches may apply heuristic freshness based on `Last-Modified`.
- A cached response that carries `Set-Cookie` can hand one user's session to another.
- Errors and redirects can be cached too; a 404 during a rolling deploy may stick.
- Purging the CDN does not clear browser caches, so a long `max-age` on a stable URL cannot be taken back.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each response class shows the intended headers through the real edge, revalidation returns 304, and a second user never receives the first user's data.
