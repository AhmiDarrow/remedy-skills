---
name: cross-platform-paths
version: 1.0.1
description: >
  Fix path and filename bugs across Windows, macOS and Linux: joining, case, reserved names, length limits and traversal. Use when file code works on one OS only or accepts names from outside.
author: Remedy Official
license: Apache-2.0
tags:
  - windows
  - quality
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: cross-platform-paths
  official: true
  security_flags: []
---

# Cross Platform Paths

## When to use
Paths break on another platform, or user-supplied names reach the filesystem.

## Steps
1. Search for paths built with string concatenation or splitting on `/` or `\`, hard-coded drive, home or temp folders, and shell commands containing paths.
2. Use the language's path library (Python `pathlib`, Node `path`, Rust `Path`). Keep URLs, archive entry names and object keys separate; they are not OS paths.
3. Use platform APIs for home, config, cache and temp locations. Resolve bundled files from the program's location, not the current directory.
4. Check case: match the exact spelling on disk, since Linux is usually case-sensitive while Windows and default macOS usually are not. Find names differing only by case.
5. For names you create, handle Windows rules: reserved characters, device names such as CON, NUL, COM1 and LPT1 even with an extension, trailing dots or spaces, and long paths.
6. For untrusted relative names, reject absolute and drive-relative forms, resolve against the base and then check containment by path components (such as `is_relative_to`), not string prefix. Joining an absolute second part can discard the base.
7. Consider symlinks and replacement between check and use; open safely where the platform provides it.
8. Handle spaces, non-ASCII names and Unicode normalisation differences. Pass paths to processes as separate arguments.
9. Test on each target OS or CI runner, including traversal and reserved-name cases.

## Watch out for
- Path libraries follow the host's rules, so a Windows-style input is not parsed as such on Linux.
- Replace-on-rename can fail on Windows when the file is open.
- Executable bits and permissions do not carry across the same way.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Tests pass on the targeted systems, escapes from the base folder are rejected, and untested platforms are named.
