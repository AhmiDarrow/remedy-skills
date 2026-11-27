---
name: encoding-fix
version: 1.0.1
description: >
  Diagnose and repair garbled text and decode errors by inspecting bytes, finding the wrong decode step and fixing it at source. Use for mojibake, UnicodeDecodeError, stray BOM characters or replacement symbols.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - debug
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
  - grep
metadata:
  source: library
  library_id: encoding-fix
  official: true
  security_flags: []
---

# Encoding Fix

## When to use
Text shows sequences like "Ã©" or "â€™", shows replacement characters, or a program fails to decode a file.

## Steps
1. Copy the affected files and inspect raw bytes before editing: `xxd file | head` or, in PowerShell, `Format-Hex file`. Terminals and editors can mislead.
2. Read the bytes. `EF BB BF` is a UTF-8 BOM; `FF FE` or `FE FF` suggests UTF-16; "é" as `C3 A9` is UTF-8, as lone `E9` is a Latin-1 or Windows-1252 style byte.
3. Test strict decoding (`iconv -f utf-8 -t utf-8 file > /dev/null`) and note the first failing offset. Guessers are only hints; confirm with a word whose correct spelling is known.
4. Trace the pipeline (source, read, transport, database, response header, display) and find the first stage where text goes wrong.
5. Interpret the symptom: "Ã©" usually means UTF-8 bytes decoded as Windows-1252 and saved again; a replacement character or "?" stored in data means information was probably lost, so recover from an earlier source.
6. Fix the faulty step with an explicit encoding (`open(path, encoding="utf-8")`, `utf-8-sig` to accept a BOM), correct charset headers and database connection and column settings.
7. Repair damaged data separately: reverse the exact wrong round trip on a copy, only for rows showing the damage, and review samples and counts before replacing anything.
8. Standardise on UTF-8, keeping a BOM or legacy encoding only where a consumer requires it.
9. Add a byte-level test fixture with accents, a curly quote, non-Latin text and an emoji.

## Watch out for
- `errors="ignore"` or `iconv -c` silently deletes characters.
- Applying the repair to already correct rows damages them, and some text is double-encoded more than once.
- Defaults differ by operating system and shell version, including redirected output on Windows.
- MySQL's `utf8` alias has historically meant a three-byte subset; check for `utf8mb4`.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The failing stage is identified from bytes, it reads and writes with an explicit correct encoding, the fixture round-trips unchanged, and any unrecoverable or still-damaged data is counted and reported.
