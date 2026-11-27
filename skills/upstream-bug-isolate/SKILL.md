---
name: upstream-bug-isolate
version: 1.0.0
description: >
  Prove a failure lives in a third-party library, report it well and keep a contained workaround. Use when the evidence points at a dependency and not at your own code.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - debugging
  - open-source
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - write
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: upstream-bug-isolate
  official: true
  domain: tooling
  security_flags: []
---

# Upstream Bug Isolate

## When to use
Your inputs look valid, yet a dependency returns wrong results or crashes. Claims like this need stronger proof than usual.
## Steps
1. Read the dependency's documentation for the installed version and confirm your usage is allowed.
2. Write a standalone program using only that library with literal inputs. If it does not fail, the problem is in your usage or environment.
3. Test the latest release and, if practical, the previous ones to learn whether it is fixed or newly broken.
4. Search the project's open and closed issues and changelog using the exact error text.
5. Read the source at the failing frame and state the suspected defect if you can see it.
6. Choose containment: upgrade, pin to the last good version, a small wrapper that avoids the bad path, or a documented patch applied by the package manager's own override mechanism. Avoid hand-editing installed files.
7. Put the workaround in one place with a comment linking the issue and the condition for removing it.
8. Add a test that fails if the workaround is removed while the bug persists.
9. Draft the upstream report: versions, platform, the standalone program, expected and actual. Strip private names, paths and data. Post only after the user approves.
## Watch out for
- Pinning forever and silently missing security fixes; record when to revisit.
- Reporting with your whole application as the reproduction.
- A fork with no plan for staying in sync.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A standalone program demonstrates the fault on a stated version, your product is protected by a tested, removable workaround, and the report is drafted or linked.
