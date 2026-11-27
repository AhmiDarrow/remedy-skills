---
name: undo-redo-implementation
version: 1.0.0
description: >
  Add undo and redo to an editor or canvas with the right history model, action grouping and collaboration limits. Use when users need to reverse edits in a design, text or board tool.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - state
  - architecture
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: undo-redo-implementation
  official: true
  domain: frontend
  security_flags: []
---

# Undo Redo Implementation

## When to use
An interactive tool needs reliable undo, or the current one reverses one pixel at a time or corrupts data.

## Steps
1. Separate document state (undoable) from view state such as zoom, panel visibility and hover (not undoable). Decide on selection explicitly.
2. Check whether the editor, rich-text or collaboration library already has an undo manager, and use it.
3. Pick the model. Snapshots with structural sharing are simplest for small documents. Command objects or patch pairs (forward and inverse) suit large ones.
4. Route every document mutation through one dispatch function; a single bypass makes history inconsistent.
5. Group by user intent: one drag, one paste, one typing run broken by pauses or cursor moves, one bulk operation. Open a transaction on gesture start and commit at end, discarding it if nothing changed.
6. A new edit after undo clears the redo stack unless branching history is a requirement.
7. Bound history by memory as well as count.
8. For external effects (server delete, upload, sent message), either make them reversible with soft delete and restore, or mark a boundary and tell the user.
9. With collaboration, undo only the local user's operations against the current document.
10. Bind platform shortcuts and leave native text field undo alone while a field has focus. Add a property test: random edits, undo all, compare with the start; redo all, compare with the end.

## Watch out for
- Inverse operations that rely on array indexes break after other items move; reference ids.
- Snapshots holding references to mutable objects change retroactively.
- Autosave must treat undo as a new change that needs saving.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The random edit round-trip test passes, each listed gesture undoes in one step, and no undo silently fails to reverse something the screen implies it reversed.
