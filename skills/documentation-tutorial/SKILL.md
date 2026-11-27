---
name: documentation-tutorial
version: 1.0.1
description: >
  Write a beginner tutorial that leads to one working result, with verified steps, expected output and recovery help. Use when new users need to learn a tool or feature by doing it.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - docs
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
  - grep
metadata:
  source: library
  library_id: documentation-tutorial
  official: true
  domain: content
  security_flags: []
---

# Documentation Tutorial

## When to use
A learner needs a guided path to a first success, not reference material.

## Steps
1. Define the reader's starting knowledge and one concrete result they will have, small enough for one sitting.
2. Choose a single path. Pick the operating system and tool versions, link alternatives elsewhere, and avoid options the learner must evaluate.
3. List prerequisites with a command that checks each, and warn of cost, accounts or system changes before step one.
4. Work through it yourself in a clean directory, disposable environment or fresh project, recording every command, file edit and surprise.
5. Write numbered steps with one action each. Say where it happens and which shell, show complete file contents or unambiguous edit locations, and mark placeholders.
6. After meaningful steps, show the expected output and how it may legitimately differ. Make something visible work early.
7. Explain only enough to understand the next action.
8. Add troubleshooting from errors you actually hit or can reproduce, with exact message, cause and fix. Say how to reset and how to clean up, including billable resources.
9. Replay from a fresh start using only the written text, fix every undeclared assumption, and record the tested versions and date.

## Watch out for
- Hidden state on your machine: installed packages, environment variables, cached logins.
- Typed-from-memory output that never appeared.
- Steps that disable security checks to make things work.
- "Simply" before the step where people get stuck.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A clean replay of the written steps reaches the stated result, or any step that could not be run is explicitly labelled untested.
