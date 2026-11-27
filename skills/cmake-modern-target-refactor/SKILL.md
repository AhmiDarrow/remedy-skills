---
name: cmake-modern-target-refactor
version: 1.0.0
description: >
  Refactor a CMake build to target-based usage requirements with working install and find_package. Use when include paths and flags leak globally or consumers cannot link your library.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - cmake
  - cpp
  - build
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
  - grep
metadata:
  source: library
  library_id: cmake-modern-target-refactor
  official: true
  domain: tooling
  security_flags: []
---

# Cmake Modern Target Refactor

## When to use
A CMake project relies on directory-wide commands and fragile variables.
## Steps
1. Record `cmake --version` and the declared minimum. Build and test the current state as a baseline, keeping a verbose command log (`cmake --build build --verbose`).
2. Find global commands: `include_directories`, `link_directories`, `add_definitions`, edits to `CMAKE_CXX_FLAGS`, and `file(GLOB` for sources.
3. Convert one target at a time to `target_include_directories`, `target_compile_definitions`, `target_compile_options` and `target_link_libraries`.
4. Choose scope per entry: PRIVATE for implementation only, PUBLIC when public headers need it too, INTERFACE for consumers only.
5. Express the language level with `target_compile_features(tgt PUBLIC cxx_std_17)` or the project's standard.
6. Link imported targets (`Foo::Foo`) from `find_package` instead of raw variables and paths.
7. Keep warning-as-error flags out of the exported interface; put them in presets or a developer option.
8. For installable libraries use `BUILD_INTERFACE` and `INSTALL_INTERFACE` expressions, `install(TARGETS ... EXPORT)` and a package config file.
9. Test the consumer path: install to a temporary prefix and build a tiny separate project using `find_package` with `CMAKE_PREFIX_PATH`.
## Watch out for
- Stale `CMakeCache.txt` can make a broken change appear to work; configure into a fresh directory.
- A header-only target must use INTERFACE scope.
- Diff the compile commands against the baseline so a dropped definition does not silently change behavior.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A fresh configure and build passes, global flag commands are gone from converted parts, and the external consumer project builds against the installed package.
