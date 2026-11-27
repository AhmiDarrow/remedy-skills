---
name: wireframe-flow
version: 1.0.1
description: >
  Sketch a low-fidelity flow for one task as screens and transitions, including branches, errors, empty states and return paths. Use before visual design or code when a flow's structure is undecided.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - ux
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: wireframe-flow
  official: true
  domain: design
  security_flags: []
---

# Wireframe Flow

## When to use
A team needs to agree what screens exist and how a person moves between them.

## Steps
1. State actor, goal, start points (navigation, deep link, email, interrupted session), finish condition, platform and preconditions such as sign-in or permission.
2. Write the shortest successful path as numbered user actions and system responses, before drawing screens.
3. List data created or needed at each step and what happens if the person lacks it.
4. Group steps into screens or dialogs. Give each an ID, name and one purpose.
5. Sketch each in plain text: headings, content blocks in priority order, real labels, controls and the primary action. Leave out colour and decoration.
6. Show transitions as a table or text diagram (a Mermaid flowchart works where it renders): from, trigger, condition, to.
7. Add branches: validation failure, system failure, timeout, no permission, empty first use, large amounts of data, cancel, back, refresh and duplicate submission.
8. For leaving midway, say what is saved and where the person resumes.
9. Walk through the flow as a first-time, a returning and an interrupted user. Mark dead ends, repeated entry and surprising irreversible steps.
10. Where a real structural choice exists, sketch two options with trade-offs, then list questions for product, engineering and visual design.

## Watch out for
- Only the successful path drawn.
- Placeholder text that hides how long or complex real content is.
- Boxes with precise styling that invite visual feedback too early.
- Inventing business rules; mark them as questions.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every screen has an ID, purpose and sketch, every action leads to a named destination including failure and exit cases, and assumptions and open decisions are listed.
