---
name: memory-forget-request
version: 1.0.0
description: >
  Carry out a user's request to forget something and report honestly where copies remain. Use when the user asks to delete, forget or stop using stored information about a topic or person.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - memory
  - privacy
kind: native
status: discovered
tools:
  - memory.search
  - memory.save
  - grep
  - read
  - edit
metadata:
  source: library
  library_id: memory-forget-request
  official: true
  domain: personal
  security_flags: []
---

# Memory Forget Request

## When to use
The user wants information removed from what you retain.

## Steps
1. Pin down the scope: one fact, a topic, a person, a time range, or "stop using it" versus delete.
2. Search memory with names, synonyms, nicknames, project labels and related facts, because details hide inside entries about other things.
3. Show the matches with minimal repetition of sensitive content and confirm what goes.
4. Remove entries with the deletion method the memory store provides. If your available tools cannot delete, say so plainly and tell the user how to remove them; saving a "forgotten" note is not deletion.
5. For mixed entries, rewrite to keep unrelated facts and drop the targeted ones.
6. Search accessible notes, indexes and summaries derived from the entry, and ask before editing user files.
7. List places you cannot reach or have not changed: backups, transcripts, synced devices, sent mail.
8. If a rule is needed to avoid re-learning it, store a neutral one that does not repeat the sensitive detail.
9. Search once more to verify.

## Watch out for
- Writing "forget that Ahmi has X" stores X again.
- Never claim data is erased everywhere when you only know about one store.
- Deleting files or bulk entries is destructive; confirm the exact list first.
- Do not argue for keeping the information or ask why it should go.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A new search returns none of the confirmed items, or the user has an accurate list of what remains and how to remove it.
