---
name: self-hosted-runner-setup
version: 1.0.0
description: >
  Set up a self-hosted CI runner with isolation, minimal credentials, cleanup and monitoring. Use when hosted runners are too slow, costly or cannot reach required hardware or networks.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - ci
  - security
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
metadata:
  source: library
  library_id: self-hosted-runner-setup
  official: true
  domain: ops
  security_flags: []
---

# Self Hosted Runner Setup

## When to use
Builds need your own machine: special hardware, a private network, large local caches or lower cost.

## Steps
1. Write down which repositories and workflows may use it. If any accept outside pull requests, use disposable machines per job or do not connect them.
2. Prefer ephemeral runners that register, take one job and are destroyed. If the machine must persist, treat anything one job leaves behind as visible to the next.
3. Put it in its own VM and network segment. Block access to your LAN, management interfaces and the cloud metadata endpoint unless a job needs them.
4. Run the agent as a dedicated unprivileged user with no sudo. Remember that membership of the `docker` group is effectively root.
5. Use the registration token from the CI system's own setup page; the user enters it. Do not save it in scripts or images.
6. Install the agent as a service (systemd, launchd or a Windows service) so it survives reboot.
7. Add labels that describe capabilities, and restrict which repositories can target the runner group.
8. Clean the workspace after each job, prune container images and volumes on a schedule, and alert on low disk and on the runner going offline.
9. Plan agent and OS updates; outdated agents can stop receiving jobs.

## Watch out for
- Mounting the container socket into job containers lets any job control the host.
- Persistent runners accumulate global tools, so builds start depending on state nobody declared.
- A shared runner with deploy credentials on disk turns every workflow that can target its label into a deployer.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A test job runs under the unprivileged user, cannot reach a blocked internal address, the workspace is clean afterwards, and the runner returns by itself after a reboot.
