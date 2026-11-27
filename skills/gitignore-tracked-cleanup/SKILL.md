---
name: gitignore-tracked-cleanup
version: 1.0.0
description: >
  Fix a repository that tracks build output or local files, or whose ignore rules do not behave. Use when ignored files still show changes or generated clutter keeps getting committed.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - repo-hygiene
  - gitignore
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
metadata:
  source: library
  library_id: gitignore-tracked-cleanup
  official: true
  domain: git
  security_flags: []
---

# Gitignore Tracked Cleanup

## When to use
Adding a line to `.gitignore` appears to do nothing, or diffs are full of machine-specific files.
## Steps
1. List tracked files that match ignore rules: `git ls-files -ci --exclude-standard`. Ignore rules never affect already tracked files.
2. For a surprising case, run `git check-ignore -v --no-index path` to see which file and line decides.
3. Sort offenders into generated output, dependencies, editor or OS files, local config, and files intentionally committed despite matching.
4. For files that should leave version control but stay on disk, use `git rm --cached` per path (`-r` for directories). Warn that others who pull will have those files deleted from their working trees, so local config needs backup and an example template.
5. Place rules correctly: project artefacts in `.gitignore`, personal editor clutter in the user's global excludes file, one-clone rules in `.git/info/exclude`.
6. Remember rule order: later lines win, and a file cannot be re-included if its parent directory is excluded. Exclude `dir/*` and then negate the exception.
7. Before any cleanup, dry run with `git clean -ndX` and read the list.
8. Verify with a fresh clone that the project builds without the removed files.
## Watch out for
- Broad patterns such as `lib/` or `*.config` that hide real source in new folders.
- Untracking a lock file or committed generated code that builds depend on.
- Assuming removal erases secrets from history; rotate them.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
No unintended tracked file matches an ignore rule, new build output stays untracked, and a clean clone still builds.
