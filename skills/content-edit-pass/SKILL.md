---
name: content-edit-pass
version: 1.0.1
description: >
  Line and copy edit a draft for clarity, concision and consistency while keeping the author's voice and meaning. Use when a user asks to edit, tighten or proofread something already written.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - writing
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
metadata:
  source: library
  library_id: content-edit-pass
  official: true
  domain: content
  security_flags: []
---

# Content Edit Pass

## When to use
The structure is broadly settled and the prose needs editing.

## Steps
1. Agree the depth: proofread only, copy edit, or line edit with reordering. Note reader, length limit, house style and spelling variety. Do not exceed the agreed depth.
2. Read it all before changing anything. State the main point in a sentence; if you cannot, say the problem is structural and raise it first.
3. Mark protected text: quotations, legal wording, code, commands, names and the author's deliberate stylistic habits.
4. For line editing, fix order within sections, move the point forward, and cut repetition. Name the actor and use verbs where noun phrases hide them.
5. Resolve unclear "this" and "it", stacked modifiers and sentences carrying several ideas. Do not shorten away a condition or hedge.
6. Make a term sheet for spelling, capitalization, hyphenation, numbers, units and product names, then `grep` for variants.
7. Check internal consistency: dates, sums, list counts, headings and cross-references.
8. Do not silently correct facts or guess an ambiguous meaning; add a query with the possible readings.
9. Deliver the edit in a reviewable form (tracked changes or a diff, keeping the original), with a short list of recurring patterns and the author queries.

## Watch out for
- Replacing the author's words with your favourites.
- Introducing errors while rephrasing: "may" becoming "will", a lost "not".
- Changing text inside quotation marks.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The draft is edited at the agreed depth, every change can be reviewed against the original, terms are consistent, and open questions are listed.
