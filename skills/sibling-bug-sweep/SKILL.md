---
name: sibling-bug-sweep
version: 1.0.0
description: >
  After diagnosing a bug, search the codebase for other instances of the same mistake and fix the class. Use when a fixed defect came from a pattern likely repeated elsewhere.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - debugging
  - code-quality
kind: native
status: discovered
tools:
  - grep
  - glob
  - read
  - edit
  - bash
metadata:
  source: library
  library_id: sibling-bug-sweep
  official: true
  domain: testing
  security_flags: []
---

# Sibling Bug Sweep

## When to use
The cause was a habit or a misunderstanding (unchecked return, timezone-naive date, unescaped input), so one fix is probably not enough.
## Steps
1. Describe the mistake abstractly in one sentence: which operation, which missing condition, what consequence.
2. Check the callers of the function you fixed. If the flaw is in shared code, fix it there once instead of at each call site.
3. Search by several angles: the API name, aliases and wrappers of it, the copied code shape, and sibling modules for other platforms or formats. Use structural search such as ast-grep when text search is too noisy.
4. Use `git log -S "snippet"` to find where the original was copied from and when.
5. List every hit with a verdict: same bug, safe because of a stated guard, or unsure. Read the surrounding code before judging.
6. For unsure hits, write a quick test with the triggering input.
7. Fix confirmed ones, with tests where behaviour differs.
8. Prevent reintroduction by the strongest cheap means: change the API so misuse cannot compile or run, add a lint rule, or add a test that scans for the banned call.
9. Report hits you chose not to fix and why.
## Watch out for
- A blind search-and-replace that breaks a site where the original behaviour was intentional.
- Searching only your own language while scripts, queries or config share the flaw.
- Growing the bug fix into a general cleanup that is hard to review.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every search hit has a recorded verdict, confirmed siblings are fixed or ticketed, and a guard against the pattern exists or its absence is explained.
