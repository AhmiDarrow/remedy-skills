---
name: module-interface-design
version: 1.0.0
description: >
  Design a module's public surface so callers need little knowledge and internals stay free to change. Use when creating a new module or library boundary, or when callers must call things in a fragile order.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - architecture
  - api-design
kind: native
status: discovered
tools:
  - read
  - grep
  - write
  - edit
metadata:
  source: library
  library_id: module-interface-design
  official: true
  domain: backend
  security_flags: []
---

# Module Interface Design

## When to use
The boundary is about to be fixed by its first callers, or current callers repeat the same setup and cleanup dance.
## Steps
1. Write the calling code you wish existed for the two or three main use cases before designing types.
2. Name the secret the module keeps: storage format, protocol, retry policy, library choice. Nothing in the surface should reveal it.
3. Collapse mandatory sequences (init, then configure, then open) into one operation that returns a ready object, or use types that make wrong order impossible.
4. Prefer few operations that do whole jobs over many thin pass-throughs.
5. Decide for each failure whether the module handles it or the caller must; return errors in domain terms, not leaked library exceptions.
6. State ownership and lifetime: who closes, whether it is safe to call from several threads, whether returned data may be mutated.
7. Make required inputs required and give the rest safe defaults. Replace boolean pairs with named options.
8. Sketch a second plausible implementation (in memory, another backend); anything in the interface it cannot honour is a leak.
9. Export only what the sample callers need.
## Watch out for
- Mirroring the underlying library one method at a time, which adds a layer and hides nothing.
- Generic plugin points for imagined callers.
- Getters exposing internal collections that callers then modify.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The main use cases read as short calls with no required hidden ordering, and failures, ownership and thread safety are documented on the surface.
