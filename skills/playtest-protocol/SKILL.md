---
name: playtest-protocol
version: 1.0.1
description: >
  Plan and run a game playtest with testable questions, neutral facilitation, timestamped observation and ranked fixes. Use when checking whether players understand, enjoy or can finish a build.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - research
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: playtest-protocol
  official: true
  domain: gaming
  security_flags: []
---

# Playtest Protocol

## When to use
A build needs evidence from players about onboarding, difficulty, clarity or enjoyment.

## Steps
1. Write two to four questions, each with the observation that would answer it, for example "can a new player craft a first item unaided?".
2. Match testers to the question. First-time questions need people who have never seen the game, and each is a first-timer only once. Record genre experience.
3. Fix the build and record its version. Play the tested path yourself from a clean save; set up save states for later sections.
4. Prepare consent for any recording, say what is kept and for how long, and get a guardian's consent for minors.
5. Write the script. State that the game is being tested, not the player. Give goals ("see how far you get"), never control hints.
6. Decide in advance when to help, such as stuck for a set time or blocked by a bug, and mark every assist.
7. Log timestamp, location, what the player did, what they said and any inference, kept separate. Track deaths, retries, help requests and quit points.
8. Debrief with open questions: what they were trying to do, what confused them, what they would do next. Collect opinions after behaviour.
9. Group findings across players. Rank by effect (blocks progress, misleads, annoys) and how many of those who reached that point hit it.
10. Give each fix an owner and the observation that will show it worked. Save notes where the project keeps them, under tester ids rather than names.

## Watch out for
- Explaining or defending the design during play.
- Treating "it was fun" from friends as evidence over what they actually did.
- Reporting percentages from a handful of players; give counts.
- Adopting a player's proposed solution without finding the problem behind it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each question is answered, unanswered or inconclusive with timestamped evidence, and top findings have severity, count and owner.
