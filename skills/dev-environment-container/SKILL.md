---
name: dev-environment-container
version: 1.0.1
description: >
  Create a development container so contributors get a reproducible toolchain, services, ports and editor setup. Use when onboarding is manual or the project works differently on each machine.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - container tooling
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
  - web.fetch
metadata:
  source: library
  library_id: dev-environment-container
  official: true
  security_flags: []
---

# Dev Environment Container

## When to use
Contributors need the same development environment, usually through a `.devcontainer/devcontainer.json`.

## Steps
1. Collect runtime versions, system packages and setup commands from CI, lockfiles and docs. CI is the best reference for versions.
2. Choose a maintained base image with a pinned version. Put slow, stable system packages in a Dockerfile layer; check current spec keys before using them.
3. If databases or queues are needed, reference a Compose file, reusing the project's existing one, and set the service and workspace folder.
4. Use lifecycle commands for project setup, such as `postCreateCommand` installing from the lockfile. Make them safe to rerun.
5. Run as a non-root user and check files written to the bind mount keep sensible ownership.
6. Put heavy dependency or build folders in named volumes where bind mounts are slow, especially on Windows and macOS, and fix volume ownership.
7. Forward only needed ports; make servers listen so forwarding works, without publishing databases to the network.
8. Supply secrets at runtime from the user's environment or an ignored file, with an example file of fake values. Never bake them into the image.
9. Build from a clean clone with no cache, then run setup, tests and the app. Ask before large downloads. Document rebuild and non-container paths.

## Watch out for
- Host dependency folders mounted into Linux carry wrong native binaries.
- CRLF line endings break shell scripts inside the container.
- Mounting the container engine socket or running privileged gives broad control of the host.
- Check processor architecture support for images and tools.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A clean clone builds the container and runs the tests and app with documented commands, or the failing step is reported.
