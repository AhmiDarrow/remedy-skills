---
name: story-continuity-audit
version: 1.0.0
description: >
  Check a long fiction manuscript or series for contradictions in names, timeline, geography and who knows what. Use when revising a novel, serial or multi-part script.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - fiction
  - editing
kind: native
status: discovered
tools:
  - read
  - grep
  - write
  - todo
metadata:
  source: library
  library_id: story-continuity-audit
  official: true
  domain: content
  security_flags: []
---

# Story Continuity Audit

## When to use
A story spans enough chapters or episodes that the writer can no longer hold every detail.

## Steps
1. Create a story bible file with sections: characters, places, objects, timeline, rules of the world, knowledge.
2. Read in order, adding each concrete fact with its chapter location the first time it appears. On a later mention, compare instead of overwriting.
3. Use `grep` for every spelling of each name and nickname to catch variants and abandoned earlier names.
4. Build the timeline as a table of scene, in-story date or offset, and elapsed time. Check ages, pregnancies, healing injuries, seasons and travel time against it.
5. Track knowledge: for each secret, note when each character learns it. Flag anyone acting on information early.
6. Follow carried objects and injuries from scene to scene.
7. Report each conflict with both quotes and locations, severity, and the smallest fix on either side.

## Watch out for
- "Fixing" a deliberate lie, unreliable narrator or character mistake. Mark as possibly intentional and ask.
- Judging from memory of an earlier chapter; reopen it and quote it.
- Applying renames with a blind replace that hits ordinary words containing the old name.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The bible covers every named character and dated event, and each reported conflict cites both locations.
