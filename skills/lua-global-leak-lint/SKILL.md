---
name: lua-global-leak-lint
version: 1.0.0
description: >
  Catch accidental globals, nil holes and version traps in Lua code embedded in games, editors or servers. Use when scripts interfere with each other or behave differently across hosts.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - lua
  - debugging
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: lua-global-leak-lint
  official: true
  domain: tooling
  security_flags: []
---

# Lua Global Leak Lint

## When to use
Lua scripts show state bleeding between files or odd table behavior.
## Steps
1. Identify the runtime and version from the host: 5.1, LuaJIT, 5.3, 5.4 or a sandboxed dialect. Check `_VERSION` and host documentation.
2. Run `luacheck` if available, with the matching standard and the host's globals declared in `.luacheckrc`.
3. Without it, list global writes from the bytecode listing (`luac -p -l file.lua`, filtering the global set instructions for that version).
4. Add `local` to each accidental assignment, including loop helpers and functions. Declare mutually recursive locals before defining them.
5. For modules, return a local table instead of defining globals.
6. During tests, set a metatable on `_G` that errors on new undeclared globals, if the host allows it.
7. Audit arrays for nil holes. The `#` operator is only reliable on sequences; keep an explicit count or use `table.remove` instead of assigning nil.
8. Check colon versus dot calls where `self` is nil or arguments are shifted.
9. Check version-sensitive features: integer division and bit operators arrived in 5.3, `unpack` moved to `table.unpack`, and `setfenv` exists only in 5.1.
## Watch out for
- `a and b or c` returns `c` when `b` is false or nil.
- Arrays start at 1, and `ipairs` stops at the first nil.
- `pairs` order is unspecified; do not rely on it for deterministic simulation or saved output.
- Some hosts rely on specific globals as callbacks; do not make those local.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The linter reports no unintended globals, and the affected scripts run in the real host without cross-script interference.
