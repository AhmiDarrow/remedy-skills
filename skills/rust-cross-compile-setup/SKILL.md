---
name: rust-cross-compile-setup
version: 1.0.0
description: >
  Cross-compile a Rust project for another OS or CPU, including linker, sysroot and C dependency problems. Use when a target build fails at linking or the binary will not run there.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - rust
  - build
  - cross-compile
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
  - web.fetch
metadata:
  source: library
  library_id: rust-cross-compile-setup
  official: true
  domain: tooling
  security_flags: []
---

# Rust Cross Compile Setup

## When to use
You need binaries for a platform other than the build machine.
## Steps
1. Get the exact triple from the destination: CPU from `uname -m`, and libc with its version from `ldd --version`. Choose between gnu, musl, msvc or a bare-metal target accordingly.
2. Add the standard library with `rustup target add <triple>` and confirm with `rustup target list --installed`.
3. Try `cargo build --target <triple>`. A compile success followed by a link failure means you need a cross linker and system libraries.
4. Set the linker in `.cargo/config.toml` under `[target.<triple>]`.
5. For crates that build C code, also set the C compiler variables the build script reads, such as `CC_<triple_with_underscores>` and `AR_<triple>`. `cargo tree -i cc --target <triple>` shows which crates pull in the C compiler helper (without `--target` it resolves for the host).
6. For OpenSSL-style system dependencies, prefer a pure-Rust or vendored feature if the crate offers one; otherwise point pkg-config at a real target sysroot.
7. If this gets long, use a containerized cross tool or a zig-based linker wrapper, or build natively on a runner of that architecture.
8. For glibc targets, build against an older glibc than the destination has; newer symbols will fail to load.
9. Check the output with `file` or an object dumper, then run it on the real target or an emulator.
## Watch out for
- `build.rs` runs on the host. Read `CARGO_CFG_TARGET_OS` there; `cfg!(target_os)` describes the build machine.
- `-C target-cpu=native` builds for your CPU and can crash elsewhere with an illegal instruction.
- A musl static binary may have different allocator performance and DNS behavior; test those.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The artifact has the expected architecture and linkage, starts on the target, and the config needed to reproduce it is committed.
