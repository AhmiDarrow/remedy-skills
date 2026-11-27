---
name: docx-tracked-changes-review
version: 1.0.0
description: >
  Review or propose edits as tracked changes and comments so the author keeps control. Use when someone sends a redlined document or asks for edits they can accept one by one.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - word-processing
  - review
kind: native
status: discovered
tools:
  - read
  - bash
  - write
  - edit
metadata:
  source: library
  library_id: docx-tracked-changes-review
  official: true
  domain: docs
  security_flags: []
---

# Docx Tracked Changes Review

## When to use
Edits must be visible and reversible in a .docx.

## Steps
1. Keep the received file untouched and work on a dated copy.
2. Read existing markup: `pandoc --track-changes=all in.docx -o review.md` shows insertions, deletions and comments with authors.
3. List each existing change and comment with location, author and a recommendation: accept, reject, or discuss with a reason.
4. Check areas around heavy edits for broken grammar, numbering and cross-references that only appear once changes are accepted.
5. When adding edits, produce real revision markup (`w:ins`, `w:del`) through a tool that supports it, or ask the user to switch on Track Changes in their editor. Retyping text directly is not tracked.
6. Keep each revision small, one idea per change, and put reasoning in a comment.
7. Use comments, not edits, for anything that changes meaning and needs the author's judgement.
8. Open the output and confirm that rejecting all changes restores the received text and accepting all gives your intended version; compare plain-text exports of both.

## Watch out for
- Accept all can silently adopt formatting and moved text nobody reviewed.
- A clean-looking view may hide markup; check before the document goes outside the team, since deleted text and comments travel with the file.
- Do not accept or reject on the user's behalf unless asked.
- Some converters drop comments or revision authors; verify after any conversion.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every change is visible with a recommendation or rationale, and the reject-all text matches the original.
