---
name: readme-quickstart-verify
version: 1.0.0
description: >
  Prove a README quickstart works by running it from a clean copy and fixing what breaks. Use when onboarding docs may be stale or before a project goes public.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - readme
  - verification
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
  - glob
metadata:
  source: library
  library_id: readme-quickstart-verify
  official: true
  domain: docs
  security_flags: []
---

# Readme Quickstart Verify

## When to use
The quickstart was written on a machine that already had everything installed.

## Steps
1. Read the quickstart and the manifest files (`package.json`, `pyproject.toml`, `Cargo.toml`, `Makefile`). Note commands or versions that disagree.
2. Review the commands before running them. Pause for anything that installs globally, needs elevated rights, touches real services or spends money.
3. Clone into a new empty temporary directory so untracked local files cannot help.
4. Use an isolated environment (container, fresh virtual environment) where available. Record what the host already provides, because that is an unstated prerequisite.
5. Run the steps exactly as written, in the stated shell. Do not silently correct typos.
6. At each failure log the command, the error and the missing fact. Fix the README, not only your environment.
7. State expected output after the key command so readers know it worked.
8. After edits, repeat once from another clean copy.

## Watch out for
- Success caused by cached packages, global tools or environment variables already set.
- POSIX-only syntax offered to Windows users with no alternative.
- Copying real values from a local `.env` into examples; use placeholders and an example file.
- Adding a prompt character inside copyable command blocks.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A second clean run completes using only the README text and reaches the stated expected result; untested platforms are named.
