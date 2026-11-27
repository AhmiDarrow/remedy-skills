---
name: break-import-cycle
version: 1.0.0
description: >
  Remove a circular dependency between modules or packages by moving the shared piece or inverting one edge. Use when imports fail by order, builds reject a cycle or two modules cannot be tested apart.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - refactoring
  - dependencies
kind: native
status: discovered
tools:
  - bash
  - grep
  - read
  - edit
metadata:
  source: library
  library_id: break-import-cycle
  official: true
  domain: backend
  security_flags: []
---

# Break Import Cycle

## When to use
Partially initialised module errors, "import cycle not allowed", or two packages that always have to change together.
## Steps
1. Get the full cycle, not one edge. Use the build error, or a tool for the language (`madge --circular` for JavaScript and TypeScript; for Python, `lint-imports` from import-linter with an `acyclic_siblings` contract for cycles between sibling packages or a `layers` contract for direction, if the installed version has them).
2. For each edge list the exact symbols used. Cycles often hang on one or two.
3. Decide which module should be lower level, meaning it should know nothing about the other.
4. Pick the fix for the wrong-direction edge: move the shared type or constant to a lower module; define an interface in the lower module that the higher one implements; pass a callback or value in at construction; or emit an event the higher level subscribes to.
5. If the two modules are really one concept, merge them.
6. For type-only references, use type-only imports (`import type`, or a `TYPE_CHECKING` guard) only when nothing needs them at run time.
7. Apply the change, run the cycle tool again, since a second path may exist.
8. Add the tool to the project checks so the cycle cannot return.
## Watch out for
- Moving the import inside a function: it hides the error and keeps the design problem.
- Creating a "common" dumping ground that soon imports from both sides.
- Barrel or index files that create cycles on their own; import from the concrete module.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The cycle tool or build reports no cycle, the lower module can be tested without the higher one, and no deferred-import hack was added to get there.
