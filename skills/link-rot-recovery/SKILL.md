---
name: link-rot-recovery
version: 1.0.0
description: >
  Recover a cited page that is dead, moved or silently changed. Use for 404 links, redirects to a home page, or a source whose text no longer matches the citation.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - research
  - sources
kind: native
status: discovered
tools:
  - web.fetch
  - web.search
  - read
  - edit
metadata:
  source: library
  library_id: link-rot-recovery
  official: true
  domain: docs
  security_flags: []
---

# Link Rot Recovery

## When to use
A reference in notes or a document no longer leads to the content it was cited for.

## Steps
1. Fetch the link and classify the failure: not found, redirect to an unrelated page, parked domain, login wall, or a live page with different text.
2. Check the URL itself for copy damage: trailing punctuation, line-break hyphens, tracking parameters.
3. Search the exact title in quotes, plus a distinctive sentence if the notes hold one. Sites often move pages without redirects.
4. For documents with a DOI, report number or ISBN, resolve by that identifier (for a DOI, `https://doi.org/` followed by it).
5. Query the web archive: `https://archive.org/wayback/available?url=` plus the encoded address returns the closest snapshot if one exists.
6. Pick the snapshot closest to the citation's access date and confirm it contains the cited claim.
7. Update the reference with the new address or archived address, keeping the original URL and access date.
8. List links with no recovery and which claims now lack support.

## Watch out for
- A 200 response can still be a "page not found" template. Read the body.
- A replacement page on the same topic is not the same source unless it contains the cited material.
- Automated checkers get blocked by some sites; a refusal does not prove the page is dead. Ask the user to open it.
- Do not send URLs containing session tokens or private document keys to an archive service.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every broken link is replaced by a verified location of the cited content or marked unrecoverable with the affected claim named.
