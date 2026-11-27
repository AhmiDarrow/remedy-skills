---
name: change-hotspot-analysis
version: 1.0.0
description: >
  Use version history to find files that change often, are complex or change together, and target refactoring there. Use when deciding where code health work will pay off most.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - architecture
  - tech-debt
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - write
metadata:
  source: library
  library_id: change-hotspot-analysis
  official: true
  domain: git
  security_flags: []
---

# Change Hotspot Analysis

## When to use
There is limited time for cleanup and opinions differ about which mess matters.
## Steps
1. Choose a window that reflects current work, such as the last 12 months. Confirm history is complete (`git rev-parse --is-shallow-repository`).
2. Count changes per file, for example `git log --since="12 months ago" --no-merges --name-only --pretty=format:` piped into a sort and unique count.
3. Exclude lock files, generated and vendored code, and release bumps.
4. Pair frequency with a size or complexity proxy such as line count or nesting depth. Files high on both are hotspots.
5. Among hotspots count fix commits using the project's message convention, and note that the signal is only as good as the messages.
6. Find coupling: count pairs of files appearing in the same commits, ignoring huge sweeping commits. Strong pairs across module borders suggest a hidden dependency.
7. Open the top handful and read them. Decide what the actual problem is, if any.
8. Report each with evidence, the specific refactor proposed and the work it would make cheaper.
## Watch out for
- Renames splitting a file's history; account for them with rename detection.
- Treating a busy but simple registry file as debt.
- Squash-merge history inflating coupling because unrelated edits share a commit.
- Ranking people instead of code; leave authors out of the report.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A short ranked list shows the churn and complexity evidence per file, notable coupled pairs, and a concrete next refactor for the ones worth it.
