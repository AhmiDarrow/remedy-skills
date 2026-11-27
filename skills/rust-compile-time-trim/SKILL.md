---
name: rust-compile-time-trim
version: 1.0.0
description: >
  Shorten Rust build times using cargo timing reports and dependency feature pruning. Use when incremental or CI builds of a Cargo project have become painfully slow.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - rust
  - build
  - performance
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
  - grep
metadata:
  source: library
  library_id: rust-compile-time-trim
  official: true
  domain: tooling
  security_flags: []
---

# Rust Compile Time Trim

## When to use
Build time hurts iteration and you want measured changes rather than folklore.
## Steps
1. Pick the scenario that hurts: clean CI build, incremental after touching a leaf file, or after touching a core crate. Measure that exact one.
2. Run `cargo build --timings` and open the HTML report. Note the longest units, the critical path, and where parallelism drops to one.
3. Find duplicate versions with `cargo tree -d` and feature origins with `cargo tree -e features`.
4. Disable default features on heavy dependencies and enable only those used. Remember features are unified across the workspace, so one crate can re-enable them for all.
5. Split a monolithic crate along real seams only if it sits on the critical path.
6. For slow linking, try a faster linker supported on your platform and toolchain, configured in `.cargo/config.toml`.
7. For dev builds, reduce debug info (`debug = "line-tables-only"` or lower in the dev profile) and compare.
8. If one crate is dominated by generics, check instantiation volume with a tool such as cargo-llvm-lines when installed, and move non-generic bodies into inner functions.
9. In CI, cache the registry and target directory keyed on lock file and toolchain, or use a compiler cache.
## Watch out for
- Trimming features can compile locally because another workspace member enables them; check each crate alone with `cargo check -p <crate>`.
- Switching compiler flags between commands (different `RUSTFLAGS` in editor and terminal) causes constant full rebuilds.
- Release profile settings such as full LTO and one codegen unit trade build time for runtime speed; do not change them unasked.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The chosen scenario is re-measured with the same command and machine, each kept change has a before and after number, and tests still pass.
