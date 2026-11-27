---
name: translation-fidelity-review
version: 1.0.0
description: >
  Review a translation against its source for meaning errors, omissions and broken variables before release. Use when translated copy or UI strings need a quality check.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - translation
  - quality
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - write
metadata:
  source: library
  library_id: translation-fidelity-review
  official: true
  domain: content
  security_flags: []
---

# Translation Fidelity Review

## When to use
A translation exists and someone must decide whether it can ship. State your confidence for the language pair up front.

## Steps
1. Obtain source and target of the same version, the glossary, the audience, and formality choice (for example informal or formal "you").
2. Run mechanical checks first: matching segment counts and keys, empty values, identical-to-source strings, and matching placeholders such as `{name}`, `%s` and HTML tags per segment.
3. Compare numbers, units, currencies, dates and negations segment by segment.
4. Check plural forms against the target language's rules; many need more than two.
5. Read the target alone for naturalness, then side by side for omissions, additions and shifted modality.
6. Verify glossary terms and untranslated brand names.
7. Check length in the real interface or note strings far longer than the source.
8. Report each issue with key, source, current text, proposed fix, severity (meaning, function, style) and certainty.

## Watch out for
- Back-translation alone: it hides awkward or wrong register that reverses cleanly.
- Translating inside placeholders, keys or code samples.
- Signing off legal, medical or safety text on your own; require a qualified native reviewer.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Placeholder and key checks pass, every meaning-level issue has a proposed fix, and uncertain items are marked for a native reviewer.
