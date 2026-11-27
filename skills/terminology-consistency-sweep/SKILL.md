---
name: terminology-consistency-sweep
version: 1.0.0
description: >
  Find and unify competing names for the same thing across a document set or product copy. Use when docs, UI and marketing call one feature by several different words.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - editing
  - terminology
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - edit
  - write
metadata:
  source: library
  library_id: terminology-consistency-sweep
  official: true
  domain: docs
  security_flags: []
---

# Terminology Consistency Sweep

## When to use
Readers cannot tell whether "workspace", "project" and "space" are one thing or three.

## Steps
1. Define the scope with `glob`: docs, UI strings, templates, help articles.
2. For each suspect concept, search all synonyms, plurals, verb forms and casing variants. Record counts and files.
3. Check the product or source of truth to learn whether the variants really are the same object. Similar words sometimes mark a real distinction.
4. Propose one preferred term per concept with a definition, banned variants and reasoning; favour what the interface already shows users.
5. Get approval before editing.
6. Replace occurrence by occurrence in context, fixing articles ("a" or "an") and grammar. Leave code identifiers, API fields, URLs, quotes and historical changelog entries as they are.
7. Where a visible rename breaks search habits, mention the old name once ("formerly called").
8. Save the term list in the repository and rerun the searches.

## Watch out for
- Global find-and-replace that rewrites file paths, anchors or translation keys.
- Renaming a heading without updating links to its anchor.
- Editing UI strings without telling whoever maintains translations that sources changed.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Searching each banned variant returns only listed, justified exceptions and the term list is committed or saved.
