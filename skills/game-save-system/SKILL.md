---
name: game-save-system
version: 1.0.1
description: >
  Design or fix game save and load with versioned data, atomic writes, backups, migrations, autosave rules and cloud conflict handling. Use when adding saving or when saves corrupt, vanish or break after updates.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - systems
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: game-save-system
  official: true
  domain: gaming
  security_flags: []
---

# Game Save System

## When to use
Player progress must survive crashes and updates.

## Steps
1. List what persists, what is recomputed and what is settings (per device or per profile). Reference content by stable ids, never object pointers, scene order or display names.
2. Define manual, auto and quick slots. Rotate autosaves and avoid saving during a state the player cannot escape.
3. Take a consistent snapshot at a safe point, then serialise and write it without concurrent mutation.
4. Add schema version, game version, timestamp and an integrity check. Parse as untrusted input with data-only formats; never use deserialisers that can construct arbitrary objects.
5. Write to a temporary file in the same directory, flush to disk, then replace the old save with the platform's atomic operation or save API, keeping the previous good copy. Web and console storage differ, so check their guarantees.
6. On load, validate; if bad, try the backup, tell the player, and keep the damaged file. Never overwrite it with a new game automatically.
7. Migrate version by version, writing a new file after backing up the original. Keep sample saves from every release as tests. Refuse saves from newer versions safely.
8. For cloud sync, detect divergence using revision history rather than clock time alone and let the player choose with meaningful details.
9. Treat local saves as editable; anything affecting rankings or purchases belongs on the server.
10. Test kill during write, full disk, read-only folder, truncated file, missing content and suspend.

## Watch out for
- Writing into the install folder.
- Reporting "saved" before the write succeeds.
- Testing against real player saves instead of copies.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Interrupted writes leave a loadable save, old sample saves migrate correctly, corrupt files are preserved with recovery offered, and untested platforms are listed.
