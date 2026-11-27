---
name: paraphrase-integrity-check
version: 1.0.0
description: >
  Help a writer find passages too close to their sources and fix attribution honestly. Use before submission when notes may have mixed copied wording with the writer's own.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - academic
  - integrity
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - write
metadata:
  source: library
  library_id: paraphrase-integrity-check
  official: true
  domain: docs
  security_flags: []
---

# Paraphrase Integrity Check

## When to use
The author wants to make sure borrowed words and ideas are credited properly.

## Steps
1. Gather the draft and the sources and notes the author actually used.
2. Compare them for shared runs of several words; a short script over word sequences works well locally. Also read side by side for matching sentence structure with swapped synonyms.
3. Flag uncited ideas, data, figures and distinctive frameworks even where wording differs.
4. For each hit, show source and draft passages together with location.
5. Let the author choose: quote exactly with a locator; paraphrase properly with a citation; summarise with a citation; or remove it.
6. For a real paraphrase, advise closing the source, explaining the point from understanding, then checking accuracy against the source. They write it.
7. Verify quoted text character by character.
8. Check reuse of their own earlier work and permission rules for figures and tables.
9. Direct unclear policy questions to the instructor, supervisor or journal.

## Watch out for
- A citation does not make unquoted copied wording acceptable.
- Standard technical terms and conventional phrases will match without being a problem.
- Never rephrase text to lower a similarity score or avoid detection.
- A comparison with only supplied sources cannot certify the draft is free of plagiarism; say that.
- Avoid uploading unpublished work to outside checkers without permission, since some retain submissions.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each flagged passage is quoted, properly paraphrased by the author and cited, or removed, and the limits of the check are stated.
