---
name: markdown-doc-structure
version: 1.0.1
description: >
  Reorganise a Markdown page or doc set so headings form a clear outline and every link and anchor still works. Use when documentation has grown messy, hard to scan or full of broken links.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
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
  library_id: markdown-doc-structure
  official: true
  security_flags: []
---

# Markdown Doc Structure

## When to use
The content is mostly there, but readers cannot find it or links are breaking.

## Steps
1. Find the renderer (repository host, static site generator) from the config. It decides anchor slugs, front matter, admonitions and whether the title comes from metadata.
2. Print the current heading tree for each file, skipping `#` lines inside code fences.
3. Before renaming or moving anything, `grep` the repository for links to these files and their `#anchors`, including code comments and in-app help URLs.
4. Name the reader and their top tasks. Order sections by that need, usually what it is, quick start, tasks, reference, troubleshooting. Split a page that mixes tutorial and reference.
5. Use one H1 (or the metadata title, never both), no skipped levels, and unique descriptive headings.
6. Move text without silently rewriting it. List anything deleted as outdated with the evidence; flag version claims you cannot verify.
7. Update inbound links. For anchors others may rely on, keep an explicit anchor or redirect if the renderer supports it.
8. Give code fences a language, keep commands separate from their output, and write link text that names the destination. Add a table of contents only if the renderer does not already.
9. Run the project's docs build or link checker. Otherwise check each relative path and anchor against the files, matching letter case.

## Watch out for
- Slug rules differ between renderers, especially for punctuation, duplicates and non-Latin text; do not assume one.
- A link that works on a case-insensitive disk can fail on the published site.
- Renumbered headings such as `3. Setup` change anchors every time a section is inserted.
- A reorganisation mixed with heavy rewording is unreviewable; keep them as separate changes.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The heading tree reads as an outline, relative links and anchors resolve, the docs build passes if there is one, and removed content is listed.
