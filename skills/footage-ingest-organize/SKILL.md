---
name: footage-ingest-organize
version: 1.0.0
description: >
  Ingest camera cards and recordings into a verified, consistently named project folder with a clip log. Use after a shoot, before editing or wiping any card.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - video
  - workflow
kind: native
status: discovered
tools:
  - bash
  - glob
  - write
  - read
metadata:
  source: library
  library_id: footage-ingest-organize
  official: true
  domain: content
  security_flags: []
---

# Footage Ingest Organize

## When to use
Media from several devices must be safe and findable.

## Steps
1. Treat cards as read-only. Never move, rename or delete on the card.
2. Create the project layout, for example `footage/<date>/<camera>/`, `audio/`, `graphics/`, `project/`, `exports/`.
3. Copy each card's whole folder structure; some camera formats need their sidecar files.
4. Verify by comparing checksums (`sha256sum` or `shasum -a 256`; `Get-FileHash` in PowerShell) between card and copy, not just file counts.
5. Make a second verified copy on a different physical drive before anyone reuses the card.
6. Probe clips into a CSV with name, duration, resolution, frame rate, codec and creation time. Flag mixed frame rates and variable frame rate.
7. Note camera clock offsets using a shared event.
8. Make proxies only if playback struggles, in a separate folder with matching names.
9. Add a short log of scene, take quality and problems. Tell the user when both copies verified; formatting the card is their action.

## Watch out for
- Duplicate names such as `C0001.mp4` from two cards overwriting each other.
- Renaming files after an edit project already links to them.
- Counting two folders on one drive as a backup.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Two copies on separate drives match source checksums and the clip log lists every media file.
