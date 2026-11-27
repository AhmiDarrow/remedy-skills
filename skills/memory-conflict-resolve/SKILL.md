---
name: memory-conflict-resolve
version: 1.0.0
description: >
  Handle stored memories that contradict each other or contradict what is true now. Use when recall returns two different answers or a remembered fact fails a live check.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - memory
  - knowledge
kind: native
status: discovered
tools:
  - memory.search
  - memory.save
  - read
  - glob
metadata:
  source: library
  library_id: memory-conflict-resolve
  official: true
  domain: personal
  security_flags: []
---

# Memory Conflict Resolve

## When to use
Memory is giving unreliable guidance.

## Steps
1. Search with several phrasings and gather every entry on the subject, not just the first hit.
2. Lay them out with date, origin and scope.
3. Check for a false conflict: different projects, machines, time periods or exceptions to a general rule.
4. Where reality can be checked, check it. A file, config, calendar or page outranks a memory about it.
5. Otherwise prefer the user's most recent explicit statement over older ones and over inferences.
6. If two explicit instructions still clash and the choice affects what you do, ask one pointed question quoting both with dates.
7. Save a replacement entry that states the current fact and what it supersedes, using whatever update or removal the memory store supports.
8. If the old entry cannot be removed, make the new one say it is obsolete, so later recall can tell which wins.
9. Search again to confirm what a future session will find.

## Watch out for
- Newest is not decisive when the newer entry was your guess.
- Merging two entries into a compromise invents a preference nobody stated.
- A remembered path, version or command may be stale; verify before running or recommending it.
- A security-relevant preference should never be loosened by inference.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A fresh search yields one clear current answer, or the unresolved conflict is stated to the user and not acted on silently.
