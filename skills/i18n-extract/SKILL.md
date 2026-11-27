---
name: i18n-extract
version: 1.0.1
description: >
  Move hard-coded interface text into the project's message catalogs with proper placeholders and plurals, and find missing, unused or broken locale keys. Use when localizing code or auditing catalogs.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - i18n
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: i18n-extract
  official: true
  security_flags: []
---

# I18N Extract

## When to use
User-visible strings sit in code, or locale files have drifted apart.

## Steps
1. Identify the i18n library, catalog format, key convention, source locale and any extraction command from config. Follow them; if none exists, agree on one before editing.
2. Search beyond element text: placeholders, `title`, `alt`, `aria-label`, toasts, validation messages, document titles, confirm dialogs, emails and server errors shown to users.
3. Skip logs, identifiers, test ids, protocol values and anything compared in code. If text is used as a value or key, separate the stable id from the label.
4. Move each whole sentence into one message with named placeholders. Use the library's own syntax; do not assume ICU.
5. Express counts with the library's plural support, not a one-versus-many `if`, since languages have different plural categories. Handle embedded links or bold with rich-text placeholders.
6. Format dates, numbers and currency with locale-aware APIs, not inside strings.
7. Add translator descriptions where meaning is ambiguous ("Open" as verb or state). Do not merge identical words with different meanings.
8. Compare catalogs by script: missing, extra, empty, still identical to source, and placeholder or tag mismatches. Check plural forms per locale.
9. Before deleting "unused" keys, search for dynamically built ones.
10. Run extraction, build and tests, then a pseudo-locale if possible to expose leftover literals and clipped layouts.

## Watch out for
- Translating at module load freezes the language at startup; translate at render time.
- Renaming keys discards existing translations.
- Filling gaps with unreviewed machine translation without marking it.
- Apostrophes and braces have special meaning in some message formats.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The scoped files have no remaining user-visible literals except listed exceptions, source strings render unchanged, and the per-locale gap and mismatch report is produced.
