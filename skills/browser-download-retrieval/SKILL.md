---
name: browser-download-retrieval
version: 1.0.0
description: >
  Fetch a statement, export or installer-free document from a website and confirm it is the right, safe file. Use when the user needs something downloaded from a site they use.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - browser
  - files
kind: native
status: discovered
tools:
  - computer.navigate
  - computer.snapshot
  - computer.click
  - bash
  - read
  - glob
metadata:
  source: library
  library_id: browser-download-retrieval
  official: true
  domain: tooling
  security_flags: []
---

# Browser Download Retrieval

## When to use
A file sits behind a few clicks in a web portal.

## Steps
1. Confirm the site address and what exactly is wanted: document type, period, format.
2. If sign-in is needed, let the user do it, then continue.
3. Find the file through the site's own menus. Distinguish real download controls from advertising buttons.
4. Before downloading, tell the user the filename, source site and size if shown, and get a yes.
5. Note the download folder contents, click once, then identify the new file by modification time rather than assuming the name.
6. Wait for partial-download extensions to disappear and compare size with what the site showed.
7. Check the content matches its type (for instance a "PDF" that is really an HTML login page) using the `file` command where available or by inspecting the header.
8. Open documents for reading only and confirm period, account label and page count. For executables, do not run them; verify publisher signatures or checksums from the official source and leave execution to the user.
9. Move or rename it to the agreed location without overwriting anything.

## Watch out for
- Clicking again while a download is pending produces `file (1)` copies and confusion over which is complete.
- Date filters often default to the current month.
- Statements contain sensitive data; keep them out of shared or temporary public folders.
- Do not disable browser or operating system warnings to force a download.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The verified file is at the agreed path with the correct period and format, and nothing downloaded was executed.
