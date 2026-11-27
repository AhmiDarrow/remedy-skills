---
name: practice-problem-ladder
version: 1.0.0
description: >
  Create practice problems that climb in difficulty, with verified answers kept separate. Use when a learner wants more practice on a specific skill.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - teaching
  - practice
kind: native
status: discovered
tools:
  - write
  - bash
  - read
metadata:
  source: library
  library_id: practice-problem-ladder
  official: true
  domain: personal
  security_flags: []
---

# Practice Problem Ladder

## When to use
One skill needs repetition with feedback, and existing exercises have run out.

## Steps
1. Define the skill narrowly and list the sub-moves it requires.
2. Collect a sample from the learner's course to match notation, scope and style, without copying graded items.
3. Plan the ladder: direct application; changed surface form; an added step; choosing this method over a similar one; an unfamiliar context; a find-the-error item.
4. Write two or three items per rung that differ in more than the numbers.
5. Include mixed earlier skills near the end so the method is not obvious from the heading.
6. Solve every problem independently of how you built it. Check numeric ones by computing in `bash` or substituting the answer back.
7. Look for ambiguity, missing data, multiple valid answers and unintentionally ugly or impossible values.
8. Put hints and worked solutions in a separate file or later section.
9. After the attempt, adjust: repeat a rung with a new item after errors, skip ahead when answers are quick and well explained.

## Watch out for
- Unverified answer keys teach errors with authority.
- Number-swapped clones train pattern copying, not method selection.
- Wording difficulty can masquerade as subject difficulty.
- Do not generate items meant to mirror a known upcoming assessment obtained improperly.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each item has an independently checked answer and a rung label, and solutions are hidden from the first view.
