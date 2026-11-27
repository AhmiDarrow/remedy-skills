---
name: spec-ambiguity-review
version: 1.0.0
description: >
  Review a written spec for gaps, contradictions and wording two builders would read differently. Use when a requirements doc or ticket is about to be handed to implementation.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - requirements
  - review
kind: native
status: discovered
tools:
  - read
  - grep
  - write
metadata:
  source: library
  library_id: spec-ambiguity-review
  official: true
  domain: docs
  security_flags: []
---

# Spec Ambiguity Review

## When to use
A spec reads smoothly, which is exactly when its holes go unnoticed.
## Steps
1. List every noun the spec manipulates. Check each is defined once and that no two words mean the same thing or one word means two things.
2. For each noun ask how it is created, changed, listed and deleted, and what happens to things that refer to it after deletion.
3. Underline weasel words: appropriate, quickly, usually, supports, handle, etc., if needed. Each needs a rule or a number.
4. Probe every list and limit: zero items, one, the maximum, one past it, duplicates.
5. Probe every sentence with "when": what if it happens twice, out of order, concurrently, or while offline?
6. Find passive voice that hides the actor ("the record is approved") and name who or what does it, with which permission.
7. Compare sections for conflicts, and compare the spec with current code for claims about existing behaviour that are false.
8. For each finding, write two plausible interpretations and ask which is meant; suggest replacement wording.
9. Order findings by rework cost if guessed wrong.
## Watch out for
- Redesigning the feature under the label of review. Raise design objections separately.
- Fifty typo-level notes that bury three blocking questions.
- Assuming an example is a rule; ask whether other values behave the same way.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each finding quotes the spec text, shows the competing readings and proposes wording, and the blocking ones are clearly separated from minor ones.
