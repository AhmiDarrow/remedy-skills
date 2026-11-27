---
name: ci-untrusted-pr-hardening
version: 1.0.0
description: >
  Audit workflows so code from an outside pull request cannot read secrets, push to the repository or poison later builds. Use before making a repository public or accepting fork contributions.
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
metadata:
  source: library
  library_id: ci-untrusted-pr-hardening
  official: true
  domain: security
  security_flags: []
---

# Ci Untrusted Pr Hardening

## When to use
A repository accepts pull requests from people without write access, or its workflows react to issues, comments or labels.

## Steps
1. List every workflow with its triggers, token permissions, secrets used and runner type.
2. Flag privileged triggers that run in the base repository's context, such as `pull_request_target`, `workflow_run` and comment triggers. For each, check whether it checks out or runs anything from the pull request head. Install scripts, build files and test configs all count as running it.
3. Split such jobs: an unprivileged job builds the untrusted code and uploads data; a privileged job treats that artifact as hostile input, never executes it, and only does the narrow write.
4. Grep for expression interpolation of attacker-controlled text inside run scripts: titles, branch names, bodies, commit messages. Pass them through an environment variable and quote it in the shell.
5. Set the default token to read-only and add write scopes per job.
6. Keep self-hosted persistent runners away from fork pull requests; a job can leave something behind for the next one.
7. Stop publish and deploy jobs from restoring caches or artifacts that untrusted runs can write.
8. Require approval before workflows run for first-time contributors, and put workflow files under mandatory owner review.

## Watch out for
- A label-gated check is racy if the author can push after the label is applied. Pin the run to the reviewed commit SHA.
- Masking in logs is not protection: a script can encode a secret before printing it or send it over the network.
- Reusable workflows and composite actions can hide the same pattern one level down.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every workflow reachable by an outsider is listed with proof that it runs no untrusted code alongside secrets or write tokens, or has been changed so it cannot.
