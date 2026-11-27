---
name: persona-profile
version: 1.0.1
description: >
  Build behaviour-based personas or clearly labelled proto-personas from research evidence, tied to design decisions. Use when a team needs a shared picture of distinct user groups.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - research
kind: native
status: discovered
tools:
  - read
  - write
  - grep
metadata:
  source: library
  library_id: persona-profile
  official: true
  domain: design
  security_flags: []
---

# Persona Profile

## When to use
Decisions keep being made for an imagined average user, or research needs turning into usable profiles.

## Steps
1. Ask which decisions the personas should inform. If one user type and a list of needs would do, say so.
2. Inventory evidence: interviews, observations, tickets, analytics, surveys, with dates, sample and gaps. With no user evidence, label every output a proto-persona made of assumptions.
3. Remove names and identifying details from notes. Code observations about goals, behaviours, context and obstacles, keeping a source ID on each.
4. Find the variables that change what the product should do, such as frequency, expertise, motivation, constraints or who else is involved.
5. Place participants on those variables and look for recurring patterns. Create a persona only for a pattern that implies different design choices; usually only a few result.
6. For each write context, goals, job to be done, current workflow and workarounds, frustrations, constraints including access needs, and decision factors.
7. Add quotes only if someone actually said them and consent covers the use. Remove identifying wording.
8. Mark each claim with evidence strength. Leave unsupported fields out.
9. State design implications as choices: what to prioritise, what not to build, where two personas conflict and which takes precedence.
10. List open assumptions with a way to test each, an owner and a review date.

## Watch out for
- Invented ages, hobbies, stock photos and biographies add false certainty and stereotypes.
- Demographics used as the grouping when behaviour does not differ by them.
- Turning counts from a small qualitative sample into population percentages.
- Treating one memorable participant as a whole group.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each profile is distinct in behaviour, claims trace to evidence or are marked assumption, design implications are stated, no real person is identifiable, and tests for gaps are listed.
