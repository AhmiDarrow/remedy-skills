---
name: document-version-compare
version: 1.0.0
description: >
  Find what changed between two versions of a document, including edits nobody mentioned. Use when a revised draft, contract or policy comes back and the differences matter.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - comparison
  - review
kind: native
status: discovered
tools:
  - read
  - bash
  - grep
  - write
metadata:
  source: library
  library_id: document-version-compare
  official: true
  domain: docs
  security_flags: []
---

# Document Version Compare

## When to use
Two files claim to be versions of the same document and the user needs every substantive change.

## Steps
1. Confirm which is older and keep both untouched.
2. Convert both the same way: `pandoc old.docx -t plain --wrap=none -o old.txt`, or `pdftotext -layout` for PDFs. Mixing converters creates false differences.
3. Compare with `git diff --no-index --word-diff old.txt new.txt`, which works outside a repository.
4. For PDF input, normalise line wrapping, hyphenation, headers and page numbers if they swamp the diff.
5. Check what plain text misses: tables, footnotes, headers, comments, embedded images, defined terms. For Word files also look for unresolved tracked changes.
6. Classify each change as substantive, clarifying or cosmetic. Treat any change to a number, date, name, negation, or must/may/should as substantive.
7. Detect moved blocks so a relocation is not reported as a delete plus an unrelated insert, and check whether moved text was also edited.
8. Report substantive changes with section, old wording, new wording and effect, compared against any change list supplied.

## Watch out for
- A supplied change summary or tracked-changes view may be incomplete. Diff the actual files.
- A one-word edit to a definition affects every place the term is used.
- Scanned versions need OCR first, and OCR errors will appear as changes; verify those visually.
- Say what could not be compared, such as image content.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
All substantive differences are listed with both wordings, unannounced ones are highlighted, and uncompared elements are named.
