---
name: retro-notes
version: 1.0.1
description: >
  Run a blameless retrospective for a sprint, project or release and turn it into a few owned, checkable actions. Use when a team wants to review how recent work went and what to change.
author: Remedy Official
license: Apache-2.0
tags:
  - process
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: retro-notes
  official: true
  security_flags: []
---

# Retro Notes

## When to use
A piece of work has ended or hit a milestone. For an outage with user impact, write an incident postmortem instead.

## Steps
1. Set scope and period, and open last retro's actions first. Mark each done, dropped (why) or still open.
2. Build a short factual timeline from what the user can share: goals versus delivered, dates, blockers, scope changes. Mark memories that nobody has checked.
3. Collect notes under what to keep, what hurt and what to try. Ask for input written independently before discussion so the first speaker does not set the direction.
4. Group notes into themes and pick one to three with the group by impact and ability to change them.
5. For each, ask what made the problem likely: process, tooling, information, time pressure. Rewrite person-shaped statements into conditions ("review requests waited two days with no agreed reviewer").
6. Write each action with one named owner, a date and an observable check. Frame uncertain fixes as experiments with a review date. "Communicate better" is not an action.
7. Cap actions at what the team can fit beside normal work, usually no more than three.
8. Separate what the team controls from issues to escalate, with who will raise them.
9. Draft the notes, remove remarks people would not want circulated, and save where the user chooses. Let the user share them.

## Watch out for
- Inventing sentiments or consensus when you only have one person's account; label whose view it is.
- Attributing sensitive comments by name, which stops honest input next time.
- Skipping the previous actions, which teaches the team that retros change nothing.
- Listing only problems and losing the practices worth protecting.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Saved notes show the status of earlier actions, chosen themes with evidence, and each new action has an owner, date and check.
