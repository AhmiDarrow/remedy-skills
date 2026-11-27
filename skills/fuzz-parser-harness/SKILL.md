---
name: fuzz-parser-harness
version: 1.0.0
description: >
  Build a coverage-guided fuzz harness for a parser or decoder and turn its crashes into fixed regression cases. Use when your own code reads untrusted or malformed files, messages or protocol data.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - fuzzing
  - robustness
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
  - jobs
metadata:
  source: library
  library_id: fuzz-parser-harness
  official: true
  domain: testing
  security_flags: []
---

# Fuzz Parser Harness

## When to use
Code in a project you own accepts bytes it did not create. Fuzz your own build locally, never someone else's service.
## Steps
1. Find the narrowest function that takes bytes or text and parses them, without network or disk.
2. Use the native fuzzer for the language: `cargo fuzz` for Rust, `go test -fuzz=FuzzName -fuzztime=60s` for Go, libFuzzer with `-fsanitize=fuzzer,address` for C and C++, Atheris for Python. Check the installed version.
3. Make the harness deterministic and stateless between calls. Treat documented parse errors as success; let panics, sanitizer reports and unexpected exceptions through.
4. Add oracles beyond crashes where possible, such as parse, serialise and parse again giving the same result.
5. Seed the corpus with small valid files covering different features, plus past bug inputs. Add a dictionary of format keywords or magic bytes.
6. Behind checksums or compression, fuzz the inner decoder or bypass the check only in the fuzz build.
7. Set input size, memory and time limits so hangs and blow-ups are reported. Run as a background job and watch whether coverage still grows.
8. For each finding, minimise the input with the tool's minimiser, fix the cause, and save the input as a normal test.
## Watch out for
- Catching every exception in the harness, which hides everything.
- A fuzzer stuck at the header check, running millions of useless inputs.
- Publishing crashing inputs for an unfixed flaw in shipped software; tell the owner privately first.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The harness reaches past input validation, a stated run duration completed, and each crash or hang is fixed with a saved test or recorded as open.
