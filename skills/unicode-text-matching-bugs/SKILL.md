---
name: unicode-text-matching-bugs
version: 1.0.0
description: >
  Fix bugs where visually identical or international text fails to match, sort, truncate or count correctly. Use when names, searches or filenames break on accents, emoji or other scripts.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - unicode
  - text
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
  library_id: unicode-text-matching-bugs
  official: true
  domain: tooling
  security_flags: []
---

# Unicode Text Matching Bugs

## When to use
Strings that look the same compare unequal, or text is cut or mangled although the byte encoding itself is right.
## Steps
1. Dump the code points of both strings, not just their appearance. Look for composed versus decomposed accents, non-breaking and zero-width spaces, a stray BOM and look-alike letters.
2. For equality, normalize both sides to NFC at the input boundary, or NFD consistently if the system requires it.
3. Reserve compatibility forms (NFKC) for search keys and identifiers; they fold ligatures, full-width forms and superscripts, which loses meaning in stored text.
4. For caseless comparison use full case folding (`casefold()` in Python or the platform equivalent), not lowercasing, and never use the user's locale for protocol identifiers because of cases such as the Turkish dotless i.
5. Decide what length means per limit: bytes for storage, code points, UTF-16 units (JavaScript `length`) or grapheme clusters for what a person sees.
6. Truncate on grapheme boundaries (`Intl.Segmenter` or a segmentation library), then confirm the byte limit.
7. For human-facing sorting use a locale-aware collator, and check the database column's collation.
8. If normalizing stored data, first find rows that would become duplicates under a unique key and resolve them with the owner.
9. Add fixtures: decomposed accent, emoji with joiners, right-to-left text and a combining mark at the cut point.
## Watch out for
- Stripping accents to make search work changes meaning in many languages; keep the original and use a separate key.
- Normalization does not unify look-alike characters from different scripts.
- File systems differ in whether they preserve or alter normalization form.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The failing pair behaves as intended, fixtures pass, and the normalization point is applied in one shared place.
