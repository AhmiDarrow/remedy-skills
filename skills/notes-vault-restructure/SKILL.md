---
name: notes-vault-restructure
version: 1.0.0
description: >
  Set up a simple note system, or reorganise plain-text or Markdown notes without breaking links or losing files. Use when someone wants to start organising notes or a collection has grown messy.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - notes
  - knowledge
kind: native
status: discovered
tools:
  - read
  - glob
  - grep
  - bash
  - write
  - edit
metadata:
  source: library
  library_id: notes-vault-restructure
  official: true
  domain: personal
  security_flags: []
---

# Notes Vault Restructure

## When to use
The user can no longer find things and wants a new structure applied to existing notes, or is setting up a note system from nothing. Starting from nothing, skip the numbered steps: set up one capture inbox, a few folders (projects, areas, reference, archive), a naming rule, links or tags for finding things, and a weekly time to empty the inbox.

## Steps
1. Back up the whole folder, including attachments and the app's hidden settings directory. If it is under Git, commit first. Ask them to close the app or pause sync during moves.
2. Measure: note count, folders, depth, orphans, duplicate filenames, attachment locations.
3. Identify the link styles in use: `[[wikilinks]]`, relative Markdown links, embeds, aliases.
4. Ask which retrieval has failed lately and design for that. Keep top-level folders few and defined by a rule ("active projects", "reference", "archive"); leave topics to links and tags.
5. Produce a move map of old path to new path, flagging name collisions, including ones differing only in letter case.
6. Pilot with one folder and check links.
7. Apply the map. Prefer the notes app's own move function if it rewrites links; otherwise update relative paths by script and show a dry run first.
8. Search for every link target and report unresolved ones, comparing with the count before the move.
9. Park unclear notes in a review folder rather than deleting them.

## Watch out for
- Moving files outside the app usually does not update links.
- Two notes with the same title make short wikilinks ambiguous.
- Sync conflicts during a mass move can duplicate or resurrect files.
- A taxonomy the user did not choose gets abandoned; get approval of the map first.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
File counts match the backup, no new broken links exist, and the user has the move map and an untouched backup. For a new system, the inbox, folders, naming rule and weekly review are in place.
