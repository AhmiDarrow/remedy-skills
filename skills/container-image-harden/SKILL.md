---
name: container-image-harden
version: 1.0.1
description: >
  Harden a container image build: smaller attack surface, pinned base, non-root runtime and no secrets in layers. Use when writing or reviewing a Dockerfile or before shipping an image.
author: Remedy Official
license: Apache-2.0
tags:
  - container tooling
  - devops
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: container-image-harden
  official: true
  security_flags: []
---

# Container Image Harden

## When to use
An image will run somewhere that matters, or a scan or review flagged it.

## Steps
1. Read the build file, `.dockerignore`, entrypoint scripts and deploy settings. Build the current image and record size, user and a scan result with whatever scanner is available.
2. Choose a supported minimal base that fits the runtime. Check libc compatibility before switching to Alpine, and shell or certificate needs before distroless. Pin by tag and digest, and arrange for digest updates so patches still arrive.
3. Use a multi-stage build; copy only runtime files into the last stage, leaving compilers, test data and package caches behind.
4. Install from lock files. Verify checksums of anything downloaded, and avoid piping remote scripts to a shell.
5. Keep secrets out. `ARG`, `ENV` and files deleted in a later layer remain recoverable. For build-time credentials use BuildKit `RUN --mount=type=secret`; inject runtime secrets at run time. If one leaked into a pushed image, tell the user to rotate it.
6. Exclude `.git`, env files, keys and local dependencies through `.dockerignore`. Inspect with `docker history --no-trunc` and by listing the filesystem.
7. Set `USER` to a numeric non-root id. Leave application files owned by root and read-only to that user; grant writes only to required directories.
8. Use exec-form `ENTRYPOINT` or `CMD`; wrapper scripts should end with `exec "$@"` so signals reach the process.
9. Run it as deployment should: read-only root filesystem, dropped capabilities and no privilege escalation. Run a smoke test and a stop test, then rescan.

## Watch out for
- A recursive `chown` after copying, which duplicates the layer; use `COPY --chown` where ownership must change.
- A `HEALTHCHECK` calling a tool the final image lacks. Some orchestrators ignore it and use their own probes.
- Treating a clean scan as proof; scanners miss manually copied binaries.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The image runs its smoke test as non-root, contains no secrets or build tools it does not need, and remaining scan findings are listed with reasons.
