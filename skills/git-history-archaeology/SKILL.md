---
name: git-history-archaeology
version: 1.0.0
description: >
  Find out why a line or behaviour exists by searching Git history past formatting commits, moves and renames. Use when code looks odd and you need its reason before changing it.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - history
  - investigation
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
metadata:
  source: library
  library_id: git-history-archaeology
  official: true
  domain: git
  security_flags: []
---

# Git History Archaeology

## When to use
Before deleting a strange condition, or when asked when and why something changed.
## Steps
1. Check history is complete: `git rev-parse --is-shallow-repository`. A shallow clone attributes everything to its boundary.
2. Start with `git blame -w -C -C -M -L start,end -- file` to see past whitespace changes and moved or copied lines.
3. If a mass reformat dominates, pass `--ignore-rev <sha>`, or use the repo's `.git-blame-ignore-revs` file with `--ignore-revs-file`.
4. Trace a function over time with `git log -L :funcName:path`, or a line range with `-L start,end:path`.
5. Find where a string appeared or vanished with `git log -S "text" --oneline --all`; use `-G regex` for changes that edit lines containing it.
6. Follow a renamed file with `git log --follow -- path`; find deleted files with `git log --diff-filter=D --name-only`.
7. Read the whole commit, its tests and neighbouring commits, then the linked pull request or issue for discussion.
8. Answer with the commit hash, what it changed and the stated reason. Mark any reason you inferred as inference, and check whether the original condition still applies.
## Watch out for
- Stopping at the latest commit, which only moved or reindented the line.
- Reading a vague commit message as proof of intent.
- Concluding a workaround is obsolete without testing the case it protected against.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The introducing commit is identified and cited, with the reason labelled as documented or inferred and a view on whether it still matters.
