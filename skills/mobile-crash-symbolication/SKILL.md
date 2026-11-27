---
name: mobile-crash-symbolication
version: 1.0.0
description: >
  Turn unreadable mobile crash reports into file and line numbers using matching dSYMs, mapping files and native symbols. Use when stack traces show addresses or obfuscated names.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - mobile
  - debugging
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: mobile-crash-symbolication
  official: true
  domain: tooling
  security_flags: []
---

# Mobile Crash Symbolication

## When to use
A release build crashes and the trace is hexadecimal addresses, single-letter classes or an unmapped JavaScript bundle.

## Steps
1. Record app version, build number, platform, architecture and the raw trace. Symbols must come from that exact build.
2. iOS: read the binary image UUID in the report and find the matching dSYM, comparing with `dwarfdump --uuid`. Symbolicate in Xcode or with `atos -o <dSYM binary> -arch <arch> -l <load address> <address>`.
3. Android Java or Kotlin: use that release's `mapping.txt` with the `retrace` tool.
4. Android native: use unstripped `.so` files with the matching build id and `ndk-stack` or `llvm-symbolizer`.
5. React Native: apply the source map for that bundle, combining Hermes and packager maps as the version requires.
6. Flutter built with `--split-debug-info`: use `flutter symbolize` with the saved symbol file for that architecture.
7. Read the symbolicated crash: exception type, crashing thread, first frame in your code, and other threads for deadlock or memory pressure.
8. Reproduce under the same OS and conditions before claiming a cause.
9. Fix the pipeline: archive all symbol files per build in release automation and upload to the crash service already used.

## Watch out for
- Rebuilding the same commit does not guarantee matching symbols; only the archived ones are reliable.
- Optimised code inlines functions, so line numbers can point near rather than at the fault.
- Out-of-memory and watchdog kills may produce no ordinary crash report.
- Reports can contain personal data; do not paste them into public places.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The top app frames resolve to source lines consistent with that version's code, and symbol archiving for future builds is verified or reported as missing.
