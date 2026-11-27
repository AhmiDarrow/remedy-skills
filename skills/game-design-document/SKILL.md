---
name: game-design-document
version: 1.0.1
description: >
  Draft or repair a lean game design document with testable pillars, core loop, systems, vertical slice scope, risks and open questions. Use for a new concept or to reconcile conflicting design notes.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - design
  - docs
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
metadata:
  source: library
  library_id: game-design-document
  official: true
  domain: gaming
  security_flags: []
---

# Game Design Document

## When to use
A game concept needs to be written down, or documents and build disagree.

## Steps
1. Read existing notes, prototypes and data. Use the project's file and format; otherwise propose `docs/gdd.md`. Ask for team size, time, budget and platforms before sizing scope.
2. Write the pitch in one sentence, then audience, platform, session shape and what makes it worth choosing.
3. Set about three pillars that can reject ideas. "Fun combat" cannot; "every fight is winnable without damage by reading tells" can. Give one example each of in and out.
4. Describe the core loop with player verbs, decisions, rewards and what sends the player round again, then session and long-term goals.
5. For each system give purpose, pillar served, key rules, dependencies, owner and status: proposed, prototyped or confirmed. Keep volatile numbers in data files and link them.
6. Define the vertical slice: exact content and quality, the questions it answers, measurable pass criteria and what is deliberately absent.
7. List non-goals, then risks, each with the cheapest test that would retire it and a date or decision owner.
8. Surface contradictions between sources as questions instead of choosing silently. Add a short decision log.

## Watch out for
- Pages of lore and feature wish lists before anyone knows what the player does each minute.
- A "vertical slice" that includes every system.
- Presenting your inventions as agreed design; mark proposals.
- Borrowed descriptions ("like game X") with no statement of which part is meant.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A teammate can list the pillars, loop, slice contents and pass criteria from the document, and undecided items have owners.
