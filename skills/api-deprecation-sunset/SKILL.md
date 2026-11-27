---
name: api-deprecation-sunset
version: 1.0.0
description: >
  Retire an API endpoint, field or version using usage data, announced dates, warning headers and staged shutoff. Use when removing something external or cross-team callers may still depend on.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - api
  - deprecation
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - write
  - edit
metadata:
  source: library
  library_id: api-deprecation-sunset
  official: true
  domain: backend
  security_flags: []
---

# Api Deprecation Sunset

## When to use
You want to delete or replace part of an API and cannot update all of its callers yourself.

## Steps
1. Define the exact surface: routes, methods, fields, parameters, enum values.
2. Measure who uses it from access logs or metrics, grouped by caller identity or API key. If you cannot tell, add that instrumentation first and collect at least one full business cycle, including monthly jobs.
3. Search your own repositories for clients, SDKs, scripts and documentation examples.
4. Ship the replacement and prove it covers each observed use, including odd parameter combinations found in logs.
5. Write the migration note with before and after requests, behaviour differences, and the removal date.
6. Signal in-band: the `Deprecation` (RFC 9745, a value like `@1688169599`) and `Sunset` (RFC 8594, an HTTP date) response headers, a link to the note, and the deprecation flag in the OpenAPI or schema file.
7. Draft messages to remaining callers; let the user approve before anything is sent.
8. Near the date, run announced brownouts: short planned windows that return the final error, so hidden dependants surface while rollback is one switch.
9. Shut off behind a flag, return 410 Gone with a pointer to the replacement, watch error rates, and delete the code only after a quiet period.

## Watch out for
- Field usage is invisible in route-level logs. For response fields you may only learn from callers, brownouts or client code.
- Health checks and your own tests can make a dead endpoint look alive, or hide that real callers are the only traffic.
- Old mobile app versions keep calling for months after the new release.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Usage by each known caller is zero or explicitly accepted by an owner, the endpoint returns the final response, and docs and schema no longer advertise it.
