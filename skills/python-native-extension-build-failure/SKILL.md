---
name: python-native-extension-build-failure
version: 1.0.0
description: >
  Diagnose a failing Python package install that tries to compile native code. Use when pip or uv errors with compiler, header, linker or metadata-generation messages.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - python
  - build
  - dependencies
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
  - web.fetch
metadata:
  source: library
  library_id: python-native-extension-build-failure
  official: true
  domain: tooling
  security_flags: []
---

# Python Native Extension Build Failure

## When to use
An install ends in a long compiler log, "subprocess-exited-with-error", or a missing header file.
## Steps
1. Ask why it is compiling at all. Look at whether the installer downloaded a `.tar.gz` instead of a `.whl`; that is usually the real problem.
2. Print the interpreter version, architecture (`python -c "import platform,sys;print(platform.machine(),sys.version)"`) and OS. Check the package's file list on its index for a wheel with matching tags.
3. Prefer getting a wheel: upgrade the installer, choose a package version that ships one for this interpreter, or use an interpreter version the package supports. Test with `--only-binary=:all:`.
4. Note libc: Alpine uses musl, so manylinux wheels do not apply and only musllinux ones do. A Debian-based slim image is often the simplest fix.
5. If building is required, read the first error in the log, not the last line. Re-run with `-v` and save the output to a file.
6. Map the error to a need: missing `Python.h` means interpreter development headers; a missing library header means that library's `-dev` or `-devel` package; "cargo not found" means a Rust toolchain; on Windows, a missing compiler means the C++ build tools.
7. If the linker cannot find a library, check `pkg-config --libs <name>` and the variables the package documents for custom paths.
8. Record the system packages in the Dockerfile or setup script so the next machine does not repeat the hunt.
## Watch out for
- An x86_64 interpreter on an ARM machine under emulation selects different wheels than a native one.
- Installing system packages with administrator rights changes the machine; show the command and ask first.
- Do not downgrade the package silently just to find a wheel; old versions may carry known vulnerabilities.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The package imports in a clean environment, and the cause (no wheel, missing header or toolchain) plus the fix is written into the project's setup steps.
