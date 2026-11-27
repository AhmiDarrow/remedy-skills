---
name: design-interview-before-build
version: 1.0.0
description: >
  Interview the user one decision at a time before building, until the design has no silent guesses. Use when a build request is vague, large or hard to undo and the user wants it pinned down first.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - planning
  - design-interview
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - write
metadata:
  source: library
  library_id: design-interview-before-build
  official: true
  domain: tooling
  security_flags: []
---

# Design Interview Before Build

## When to use
A request such as "build me a sync feature" hides a dozen choices. Run this before code, not after the first wrong version.
## Steps
1. Read the repo first. Every question the code, config or docs can answer is not a question for the user; write those answers down with the file path.
2. List the open decisions and sort them by what they block: data model and ownership, who uses it, failure behaviour, compatibility with existing data, then UI wording and polish.
3. Ask one decision at a time, starting with the one that changes the most downstream. Give two or three concrete options, your recommendation, and what each option costs.
4. Phrase questions as scenarios: "Ahmi edits the same note on two offline devices; which text survives?" beats "How should conflicts work?".
5. When an answer is "whatever you think", state the default you will take and record it as your choice, not theirs.
6. Probe the unhappy paths explicitly: empty input, partial failure, cancel halfway, second run, 100x the expected volume, removal or uninstall.
7. Ask what is out of scope. Capture each exclusion as a sentence.
8. Stop when a new question would not change what you build. Write a one-page summary (decisions, defaults taken, exclusions, still unknown) and ask the user to correct it before building.
## Watch out for
- Dumping fifteen questions in one message; people answer the easy three and the rest become silent guesses.
- Leading questions that only offer your preferred design.
- Treating an early answer as final after a later one contradicts it. Name the contradiction and ask which wins.
- Interviewing about a two-line change. If it is cheap to redo, build it and show it.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A written summary exists in which every blocking decision has an answer or a labelled default, and the user has confirmed or corrected it.
