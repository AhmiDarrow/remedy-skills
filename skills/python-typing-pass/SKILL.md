---
name: python-typing-pass
version: 1.0.1
description: >
  Add or tighten type annotations on chosen Python modules until the project's type checker passes honestly. Use when adopting mypy or pyright, or when type errors are being silenced instead of fixed.
author: Remedy Official
license: Apache-2.0
tags:
  - python
  - quality
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: python-typing-pass
  official: true
  security_flags: []
---

# Python Typing Pass

## When to use
Selected modules need useful static checking without a whole-codebase rewrite.

## Steps
1. Use the configured checker and its version, with the CI command. Record baseline errors and confirm the target files are actually included.
2. Start with low-dependency or boundary modules. Match annotation syntax to the minimum supported Python.
3. Group errors by cause. Fix likely real bugs first, such as unhandled `None`, wrong return types and bad calls; reproduce with a test where behaviour changes.
4. Annotate public signatures. Accept broad read-only types (`Sequence`, `Mapping`) and return precise ones. Use `TypedDict`, dataclasses or `Protocol` for structured shapes.
5. At untrusted boundaries, take `object` or the raw value and validate at runtime before narrowing. Annotations check nothing at run time.
6. For third-party gaps, install matching stub packages with approval, or write a small local stub.
7. Where an ignore or `cast` is unavoidable, make it narrow with the error code and a reason, and enable unused-ignore warnings.
8. Tighten per module, so cleaned code cannot regress, and add the check to CI.
9. Rerun checker and tests. Inspect where `Any` still flows in.

## Watch out for
- A clean result with unannotated functions may mean their bodies were not checked.
- Missing-import ignores turn whole libraries into `Any`.
- `assert` used only to narrow disappears under optimised runs, so never use it to validate input.
- Import cycles for types need `TYPE_CHECKING` guards, but runtime users of annotations must still resolve them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The target modules pass at the stated strictness, tests pass, and each remaining ignore, cast and untyped dependency is justified or listed.
