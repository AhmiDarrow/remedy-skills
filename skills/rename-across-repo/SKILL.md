---
name: rename-across-repo
version: 1.0.0
description: >
  Rename a symbol, concept or product term across a whole repository including strings, config, data and docs. Use when a rename reaches beyond what one editor refactor can see.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - refactoring
  - rename
kind: native
status: discovered
tools:
  - grep
  - glob
  - bash
  - edit
  - read
metadata:
  source: library
  library_id: rename-across-repo
  official: true
  domain: tooling
  security_flags: []
---

# Rename Across Repo

## When to use
The old name appears in code, environment variables, database columns, file names and user text, with different compatibility rules for each.
## Steps
1. Search every spelling: camelCase, PascalCase, snake_case, kebab-case, SCREAMING_CASE, spaced words, plurals and abbreviations. Use `git grep -i` plus a search of file names with `git ls-files`.
2. Classify hits: internal identifiers, public API, persisted data (columns, keys, serialised fields, file formats), operational names (env vars, metrics, flags), user-facing text, history (changelogs, old migrations).
3. Leave history and applied migrations unchanged.
4. For persisted and public names, plan an alias: read both, write new, with a stated removal point. Or keep the wire name and rename only in code through a serialisation mapping.
5. Use language-aware rename for identifiers where available; it avoids unrelated words.
6. Replace text in reviewed batches, using word boundaries. Check substrings: renaming "user" must not alter "username" by accident.
7. Rename files with `git mv`. A case-only rename needs two steps on case-insensitive file systems.
8. Preserve each file's encoding and line endings.
9. Build, test, load old saved data, then search again and justify each remaining hit.
## Watch out for
- Changing a serialised field name and silently dropping users' stored settings.
- Dashboards, alerts or scripts outside the repo that expect the old name; list them for the user.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Remaining occurrences of the old name are all on a justified list, and data and configuration created under the old name still work.
