---
name: merge-duplicate-logic
version: 1.0.0
description: >
  Unify copies of the same logic that have drifted apart, after deciding which differences are intentional. Use when the same rule is implemented in several places and a fix had to be made twice.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - refactoring
  - code-quality
kind: native
status: discovered
tools:
  - grep
  - read
  - edit
  - bash
  - write
metadata:
  source: library
  library_id: merge-duplicate-logic
  official: true
  domain: backend
  security_flags: []
---

# Merge Duplicate Logic

## When to use
Several versions of one rule exist (validation, price rounding, path handling) and they no longer agree.
## Steps
1. Find all copies by searching for distinctive constants, error messages and call patterns, since names often differ.
2. Decide whether they express the same rule. Code that merely looks alike but changes for different reasons should stay separate.
3. Tabulate the differences: inputs accepted, edge behaviour, errors, side effects.
4. Label each difference intentional, a bug in one copy, or unknown. Use blame to find fixes applied to only one copy. Ask about unknowns.
5. Write tests for the agreed behaviour and run them against every copy to see which already conform.
6. Create or pick one home at a layer all callers may depend on.
7. Migrate one caller per commit. Express real differences as explicit arguments or separate small functions, not a flag that switches half the body.
8. Delete each old copy as its last caller moves. Call out every behaviour change that a caller now experiences.
## Watch out for
- Silently adopting the first copy's behaviour for everyone.
- A shared function that grows boolean parameters until nobody can predict it; split it instead.
- Introducing a dependency from a low-level package onto a high-level one to share code.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
One implementation serves the shared rule, its tests encode the decided behaviour, and caller-visible changes are listed.
