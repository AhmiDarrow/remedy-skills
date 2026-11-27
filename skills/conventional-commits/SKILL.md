---
name: conventional-commits
version: 1.0.1
description: >
  Write Conventional Commit messages that match the actual diff, repository conventions and release tooling. Use when asked to commit or to word or fix a commit message.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - docs
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: conventional-commits
  official: true
  security_flags: []
---

# Conventional Commits

## When to use
A commit message is needed, or a message was rejected by a commit lint rule.

## Steps
1. Check conventions first: `git log -20 --format="%s%n%b"`, commit lint configuration, release automation settings and the contributor guide. Local rules on types, scopes, length and issue footers override defaults.
2. Read `git diff --cached`. If nothing is staged, inspect `git diff` and `git status`, and agree what belongs in the commit.
3. If the diff holds unrelated changes, propose separate commits and the paths for each.
4. Format the header as `<type>[optional scope][!]: <description>`. The specification defines `feat` for a new feature and `fix` for a bug fix; types such as docs, refactor, perf, test, build, ci and chore are common additions that the project may restrict.
5. Pick by effect on users of the code: a change that repairs behaviour is `fix` even if it looks like a refactor. A pure restructure must not change behaviour.
6. Write the description in the imperative, specific enough to stand alone in a log. A short header, about 72 characters or less, is a good default.
7. Add a body after a blank line when the reason, the previous behaviour or a trade-off is not obvious from the diff.
8. Mark breaking changes with `!`, a `BREAKING CHANGE: <what breaks and how to migrate>` footer, or both. The footer token is uppercase.
9. Commit only if asked. For multi-line text, write it to a temporary file and use `git commit -F`. Check the result with `git show --stat HEAD`.

## Watch out for
- Release tools deriving version numbers from the type: a wrong `feat` or missing breaking marker ships the wrong version.
- Squash merging using the pull request title, so branch commit messages never reach the main branch.
- Inventing issue numbers or reasons not found in the diff or conversation.
- Amending a commit already pushed without agreement.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The message matches the staged diff, passes the project's rules, flags any breaking change, and is committed only if requested.
