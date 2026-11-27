---
name: transcript-cleanup
version: 1.0.1
description: >
  Turn a raw transcript into a readable, faithful document with consistent speakers, topic paragraphs, a chosen editing level, flagged doubts and redactions. Use when an interview, call or talk transcript is messy.
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
  - grep
metadata:
  source: library
  library_id: transcript-cleanup
  official: true
  domain: content
  security_flags: []
---

# Transcript Cleanup

## When to use
Text already exists but is hard to read: broken lines, filler, wrong names, unclear speakers.

## Steps
1. Ask the purpose and choose a level: verbatim (keep fillers and false starts, for legal or research use), clean verbatim (drop fillers and stutters, keep wording and grammar), or edited for reading (light repair, disclosed at the top).
2. Keep the original file untouched and write to a new one.
3. Remove caption debris: sequence numbers, rolling duplicates, mid-sentence breaks. Keep timestamps at speaker changes or every few minutes.
4. Assign speaker labels from evidence such as introductions or being addressed by name. Otherwise use Speaker 1 and Speaker 2, and mark uncertain turns.
5. Start paragraphs at topic or speaker changes. Add headings only for long recordings, clearly as editor additions.
6. Correct recognition errors using a glossary of names and terms from the user. `grep` for variant spellings. Mark unclear passages `[inaudible 00:12:34]` or `[unclear: word?]`.
7. Preserve negations, numbers, hedges and commitments exactly. List doubtful ones for an audio check.
8. Agree what to redact (contact details, account numbers, health details, third parties, off-record remarks), replace with labelled brackets, and `grep` the output for leftovers.
9. If asked, add a short summary, decisions and action items, each tied to a timestamp, with owners and dates only when spoken.

## Watch out for
- Repairing grammar can turn "we might" into "we will" or change someone's voice.
- "Yeah" meaning agreement and "yeah" as a verbal nod are different; do not turn nods into approvals.
- Quotes taken from an edited version need checking against the original before publication.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The new file states its editing level, speakers and paragraphs are consistent, every doubt and redaction is marked, summaries trace to timestamps, and the original is unchanged.
