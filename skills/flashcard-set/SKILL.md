---
name: flashcard-set
version: 1.0.1
description: >
  Turn study material into accurate, one-idea flashcards and export them for a spaced repetition app. Use when someone asks for flashcards, Anki-style cards or a self-quiz deck from notes, chapters or slides.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - learning
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: flashcard-set
  official: true
  domain: personal
  security_flags: []
---

# Flashcard Set

## When to use
Material needs to become cards that test recall.

## Steps
1. Read the source. Ask what the test or use looks like, the learner's level and roughly how many cards they can sustain.
2. Pick what is worth memorising. Concepts that need understanding get "why", "compare" and "apply to this case" cards; procedures get a card per decision point.
3. Make each card ask one thing with one defensible answer. Split lists into separate cards or cloze deletions.
4. Make each front stand alone: name the subject and context, since cards are reviewed shuffled.
5. Add reverse cards only where both directions are useful, such as vocabulary.
6. Check every answer against the source and note the page or section. Where the source looks wrong or ambiguous, ask instead of fixing silently; label anything added from outside it.
7. Remove cards answerable from the wording, yes/no cards and near-duplicates; for easily confused items add a contrast card.
8. Export in the format the app imports. For CSV or TSV: UTF-8, front, back, tags; quote fields containing the delimiter, quotes or line breaks. Suggest a test import of a few cards.
9. Advise a small daily number of new cards, answering before flipping, and rewriting cards that are failed repeatedly.

## Watch out for
- Copying whole sentences with one word blanked trains pattern matching.
- Hundreds of cards at once create a review pile that gets abandoned.
- Accented text and formulas often break on import; test those rows.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each card tests one idea, stands alone and traces to the source, and the export file parses with the same number of cards as listed.
