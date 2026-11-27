---
name: ci-action-pinning
version: 1.0.0
description: >
  Pin third-party CI steps, reusable workflows and build images to immutable digests and set up reviewed updates. Use when pipelines reference moving tags like v4, main or latest.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - ci
  - supply-chain
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - edit
  - bash
  - web.fetch
metadata:
  source: library
  library_id: ci-action-pinning
  official: true
  domain: security
  security_flags: []
---

# Ci Action Pinning

## When to use
Build or release jobs run third-party code selected by a mutable tag or branch.

## Steps
1. Grep workflow and pipeline files for `uses:`, `image:`, `FROM`, remote includes and downloaded installers. Include reusable workflows.
2. Sort by blast radius: anything in a job holding publish or deploy credentials goes first.
3. For each action, resolve the tag you use to a full 40-character commit SHA from the upstream repository, for example with `git ls-remote <url> 'refs/tags/<tag>' 'refs/tags/<tag>^{}'`. If a line ending in `^{}` appears, the tag is annotated and that line is the commit.
4. Confirm the commit belongs to the upstream repository and not only to a fork; some hosts resolve fork commits through the parent's URL.
5. Replace the reference and keep the readable version as a trailing comment.
6. Pin container images as `name:tag@sha256:...`, using the multi-platform index digest if runners differ in architecture.
7. For downloaded binaries, verify a checksum committed in your repository, not one fetched from the same place at run time.
8. Configure an update bot or a scheduled routine that proposes new pins as pull requests, and review the upstream diff before merging.

## Watch out for
- Pinning the outer action does not pin what it fetches internally: a pinned wrapper may still pull a latest image. Read its definition file.
- Pins without an update path rot and miss security fixes.
- Auto-merging bump pull requests restores the same trust in upstream that pinning removed.
- Do not invent a SHA from memory; resolve every one live.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
No privileged job references a mutable third-party tag, each pin carries its version comment, and an update mechanism has been configured.
