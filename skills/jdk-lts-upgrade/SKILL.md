---
name: jdk-lts-upgrade
version: 1.0.0
description: >
  Upgrade a JVM project across JDK releases, covering removed APIs, strong encapsulation, build plugins and bytecode tools. Use before moving to a newer long-term support JDK.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - java
  - upgrade
  - jvm
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
  - grep
  - todo
  - web.fetch
metadata:
  source: library
  library_id: jdk-lts-upgrade
  official: true
  domain: tooling
  security_flags: []
---

# Jdk Lts Upgrade

## When to use
The runtime JDK is being raised by one or more major versions.
## Steps
1. Separate three settings: the JDK running the build, the compile target (`--release`) and the production runtime. Plan which moves when.
2. Run `jdeps --jdk-internals` and `jdeprscan` over your jars and dependencies.
3. Upgrade the build tool and its plugins to versions that support the target JDK before changing the JDK.
4. Upgrade libraries that generate or rewrite bytecode: annotation processors, mocking, coverage, ORM proxies and agents. "Unsupported class file major version" points to one of these.
5. When crossing JDK 11, add explicit dependencies for the removed Java EE modules (such as JAXB) and note the `javax` to `jakarta` rename belongs to framework upgrades, a separate step.
6. For `InaccessibleObjectException`, upgrade the library first; use a narrow `--add-opens` only as a recorded stopgap.
7. Check startup flags. Removed GC or logging options can stop the JVM from launching.
8. Run on the new runtime with the old bytecode target first, then raise the target.
9. Test locale and charset sensitive behavior: UTF-8 became the default charset in JDK 18, and locale data has changed formatting between releases.
## Watch out for
- Tests may pass while a production-only agent or startup script fails; boot the real deployment artifact with its real flags.
- Libraries published by your team must not raise their target above what consumers run.
- Compiling with `-source` and `-target` instead of `--release` can link against newer APIs and fail at runtime.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The build and tests pass on the new JDK, the production artifact boots with its production flags in staging, and every remaining `--add-opens` is listed with a reason.
