---
name: ts-runtime-boundary-validation
version: 1.0.0
description: >
  Replace unsafe type assertions at TypeScript input boundaries with runtime validation that also produces the types. Use when typed code crashes on API, file, env or storage data.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - typescript
  - validation
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
  library_id: ts-runtime-boundary-validation
  official: true
  domain: backend
  security_flags: []
---

# Ts Runtime Boundary Validation

## When to use
The compiler is satisfied but production fails with undefined property access on external data.
## Steps
1. Locate boundaries: `grep` for `JSON.parse`, `.json()`, `process.env`, `localStorage`, message handlers, and `as ` casts to domain types.
2. Treat each incoming value as `unknown`. `JSON.parse` returns `any`, so annotate its result explicitly.
3. Use the validation library already in the project. If there is none and only a couple of small shapes, hand-written type guards with tests are enough; otherwise adopt one schema library.
4. Define the schema once and derive the static type from it, so the two cannot drift.
5. Decide per field how to treat reality: optional versus nullable, unknown extra keys, numbers arriving as strings, and dates as ISO text. Coerce only where documented, since coercing an empty string can yield 0 or false surprises.
6. Parse environment variables once at startup and fail with the names of all missing or invalid keys, without printing values.
7. At request boundaries, return a client error listing field paths. For third-party responses, log the failing path and handle it as an upstream fault.
8. Add fixtures with one valid payload and several broken ones (missing, null, wrong type, extra nesting).
## Watch out for
- A user-defined type guard is a promise the compiler does not check; a guard that tests one property and claims the whole type is another cast.
- Strict rejection of unknown keys on third-party data breaks you when they add a field.
- Validating deep inside business logic repeats work and misses paths. Validate at the edge and pass typed values inward.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
No external value reaches domain code through a bare assertion, and the broken fixtures are rejected with readable field-level errors.
