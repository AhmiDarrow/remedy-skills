---
name: removal-diff-review
version: 1.0.0
description: >
  Review deletions and rewrites to find behaviour, safeguards or users that disappear along with the code. Use when a change removes features, replaces a module or deletes a lot of code.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - review
  - refactoring
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - glob
metadata:
  source: library
  library_id: removal-diff-review
  official: true
  domain: git
  security_flags: []
---

# Removal Diff Review

## When to use
Deletion looks safe and satisfying, which is why lost behaviour slips through.
## Steps
1. List removed files and symbols (`git diff --diff-filter=D --name-only` for files, then read removed lines in modified ones).
2. For each removed function, inventory what it did besides its name: validation, permission check, logging that monitoring reads, cleanup, rate limit, default value.
3. Match each duty to its new home in the diff. Unmatched duties are findings.
4. Search for references that the compiler cannot see: string-based lookups, reflection, route and plugin registration, config, scripts, CI, docs, other repositories if known.
5. Check external contracts: CLI flags, config keys, file formats, endpoints, exported symbols, event names.
6. Check stored data: can records, saved files or queued jobs created by the old code still be read?
7. Review removed tests one by one. A deleted test for behaviour that still exists is lost protection.
8. Use `git log -L :name:path` or blame on odd removed lines to learn which bug they fixed.
## Watch out for
- Zero grep hits for a name that is assembled at runtime from pieces.
- Replacement code that handles the common case only.
- Leftover flags, env variables and dependencies that nothing now uses.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every removed duty is either shown in the replacement or explicitly accepted as dropped, with references and stored data checked.
