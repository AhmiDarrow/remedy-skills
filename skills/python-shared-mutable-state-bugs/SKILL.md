---
name: python-shared-mutable-state-bugs
version: 1.0.0
description: >
  Track down Python bugs caused by shared mutable objects: default arguments, class attributes, shallow copies, and late-binding closures. Use when values leak between calls or instances.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - python
  - debugging
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: python-shared-mutable-state-bugs
  official: true
  domain: backend
  security_flags: []
---

# Python Shared Mutable State Bugs

## When to use
Data from one call, request or object shows up in another, or a function behaves differently the second time it runs.
## Steps
1. Write a two-call reproduction: call the suspect twice, or build two instances, and assert the second is unaffected by the first.
2. Search for mutable defaults: `grep` for parameter defaults of `[]`, `{}`, `set()` or a constructed object. Replace with `None` and build inside the body. Linters such as the bugbear rule set flag these.
3. Check class bodies for lists and dicts assigned at class level and then mutated through `self`. Move them into `__init__`, or use `dataclasses.field(default_factory=list)`.
4. Look for `[[0] * w] * h` and `dict.fromkeys(keys, [])`. Both repeat one object; use a comprehension.
5. Check copies. `list(x)`, `x.copy()` and `{**x}` are shallow, so nested structures are still shared. Use `copy.deepcopy` only where nested mutation is really needed, or return new objects instead of mutating.
6. For callbacks created in a loop, bind the current value with a default argument or `functools.partial`; a closure reads the loop variable when called, not when created.
7. Inspect module-level caches and `lru_cache` results that return mutable objects. A caller that appends to the result poisons the cache; return a tuple or a copy.
8. Prove the culprit by comparing `id()` of the two supposedly separate objects before changing code.
## Watch out for
- Some code relies on a mutable default as a cache. Check callers before removing it, and replace it with an explicit cache.
- `+=` on a list mutates in place, while on a tuple or string it rebinds; the same line behaves differently by type.
- Test order can hide the bug. Run the failing test alone and then in the full suite.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The two-call reproduction passes, and the shared object that caused the leak is named along with the line that mutated it.
