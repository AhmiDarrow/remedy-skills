---
name: swallowed-error-audit
version: 1.0.0
description: >
  Find places where errors are caught and ignored, defaulted or logged without effect, and decide what each should do. Use when failures vanish silently or success is reported after something broke.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - error-handling
  - code-quality
kind: native
status: discovered
tools:
  - grep
  - glob
  - read
  - edit
  - bash
metadata:
  source: library
  library_id: swallowed-error-audit
  official: true
  domain: testing
  security_flags: []
---

# Swallowed Error Audit

## When to use
Users report that "nothing happened", data goes missing without errors, or a debugging session found an empty handler.
## Steps
1. Search for the language's silencing forms: bare or broad `except` followed by `pass`, empty `catch` blocks, `.catch(() => {})`, ignored `err` in Go (`_ =`), `unwrap_or_default()` and `.ok()` in Rust, shell commands followed by `|| true`.
2. Search for quieter forms: unawaited promises, ignored exit codes and return values, background tasks nobody joins, shell scripts lacking `set -e` or `pipefail`.
3. Enable linters that flag these where the project has them.
4. For each hit, ask what failure can really arrive and what the caller believes afterwards.
5. Classify: expected and harmless (narrow the catch, comment why), recoverable (fallback that is visible in logs or UI), or must propagate.
6. Prioritise handlers around writes, deletes, payments, sync, backup and config loading. A default value returned after a failed load can later overwrite the real file.
7. Narrow exception types so programming errors are not caught with expected ones. Keep the original cause when rethrowing.
8. Add a test that injects the failure and checks the visible result.
## Watch out for
- Turning every silent handler into a crash, including best-effort cleanup that should stay quiet.
- Logging and rethrowing at every layer, which floods logs with copies.
- Error messages that dump secrets or personal data.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each audited handler is justified in a comment, narrowed, surfaced or propagating, and the data-affecting ones have a failure-injection test.
