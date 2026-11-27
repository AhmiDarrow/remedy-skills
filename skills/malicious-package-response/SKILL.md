---
name: malicious-package-response
version: 1.0.0
description: >
  Respond when a compromised or typosquatted package may have been installed, scoping affected machines, secrets and builds. Use when a dependency you use is reported as malicious.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - supply-chain
  - incident
kind: native
status: discovered
tools:
  - grep
  - glob
  - read
  - bash
  - web.fetch
  - owner.notify
metadata:
  source: library
  library_id: malicious-package-response
  official: true
  domain: security
  security_flags: []
---

# Malicious Package Response

## When to use
A registry advisory or report says a package version you may use contained hostile code.

## Steps
1. Read the primary advisory: exact names, versions, publish window, trigger (install, build, import or runtime), payload behaviour and indicators.
2. Search lockfiles across all branches in use, plus built images, CI logs, artifact mirrors and package caches. Manifests with version ranges do not show what was installed.
3. Establish which machines and jobs installed it during the window.
4. Do not install, import or build the project to investigate. Inspect files statically.
5. Stop spread: pause affected pipelines and publishing, block the versions in your mirror or proxy.
6. Assume every secret readable by a process that executed it is exposed: environment variables, registry tokens, cloud and SSH keys, local config. Rotate them from a clean machine, in order of reach, after checking the advisory for payloads that react to revocation.
7. Check for follow-on effects: unexpected releases of your own packages, new workflow files, repositories, keys or outbound connections.
8. Rebuild affected hosts and runners where code ran with meaningful access.
9. Pin a known good version from a trusted source, clear caches, rebuild artifacts and redeploy.
10. Record exposure and add controls: lockfile-only installs, disabled install scripts where workable, and a delay before adopting brand-new releases.

## Watch out for
- Removing the dependency does not undo what already ran.
- Transitive dependencies are where it usually hides.
- A clean current lockfile may have been compromised in an earlier commit or CI run.
- Replacement packages suggested in comments may be a second trap.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Affected hosts and builds are listed or ruled out with evidence, exposed secrets are rotated, and shipped artifacts contain no bad version.
