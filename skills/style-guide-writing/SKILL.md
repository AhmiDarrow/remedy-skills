---
name: style-guide-writing
version: 1.0.1
description: >
  Build a house writing style guide from the team's real text: base reference, mechanics decisions, terminology, inclusive language and examples. Use when several writers produce inconsistent copy or docs.
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
  - glob
metadata:
  source: library
  library_id: style-guide-writing
  official: true
  domain: content
  security_flags: []
---

# Style Guide Writing

## When to use
Writers keep disagreeing about capitals, terms and tone, or new contributors have nothing to follow.

## Steps
1. Gather representative text with `glob` and `read`: docs, interface strings, posts, support replies. Ask which samples the team considers good.
2. `grep` for variants of the usual disputes: product and feature names, heading case, serial comma, numbers, dates, times, units, contractions, "log in" versus "login". Record counts.
3. Pick one published style manual and one dictionary as the fallback, so the house guide lists only decisions and exceptions.
4. State three or four voice principles, each as a choice with a cost ("plain over clever"), each with a before and after from the real samples.
5. Say how tone shifts for errors, billing, incidents, marketing and reference docs.
6. Decide the disputed mechanics one by one. Where the team has not chosen, offer the majority usage and ask.
7. Create a word list: preferred term, banned variants, definition, capitalisation. Spell your own product names exactly; check third-party names against their owners' usage.
8. Cover inclusive and accessible writing concretely: gender-neutral reference, person descriptions only when relevant, link text that makes sense alone, no directions that rely only on colour or position.
9. Put a one-page summary first, store the guide where writers work, name an owner and say how to propose changes. Mark which rules a linter could check.

## Watch out for
- A long guide that restates grammar nobody disputes goes unread.
- Adjectives such as "friendly and professional" decide nothing without examples.
- Applying prose rules to code identifiers, quotations or legal text that must stay verbatim.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A saved guide names its fallback references and owner, records a decision for each dispute found in the samples, includes a term list and real before-and-after examples, and open decisions are listed.
