---
name: firmware-memory-budget
version: 1.0.0
description: >
  Fit embedded firmware into flash and RAM by reading the map file and measuring stack and heap use. Use when the linker reports a region overflow or a device crashes from low memory.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - embedded
  - firmware
  - memory
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: firmware-memory-budget
  official: true
  domain: tooling
  security_flags: []
---

# Firmware Memory Budget

## When to use
Code size or RAM on a microcontroller is tight.
## Steps
1. Get region sizes from the linker script and part datasheet, accounting for bootloader and update slots.
2. Run `size` on the ELF. Flash holds code, constants and initial values of initialized data; RAM holds data, bss, stacks and heap.
3. Generate a map file (`-Wl,-Map`) and list the largest symbols with `nm --size-sort -S`. Record this baseline.
4. Find unexpected pulls: floating point formatting, full printf, C++ exceptions and RTTI, soft float double math and unused middleware.
5. Enable `-ffunction-sections -fdata-sections` with `-Wl,--gc-sections`, then compare size optimization and link-time optimization one at a time.
6. Make lookup tables and strings `const` so they stay in flash where the architecture allows it.
7. Measure stacks: use `-fstack-usage` for per-function figures and fill stacks with a pattern to read high water marks under worst-case load, including nested interrupts.
8. Review heap use. Prefer static or pool allocation where fragmentation would be fatal in long-running devices, and handle every allocation failure.
9. Add a build check that fails above a chosen margin per region.
## Watch out for
- LTO or section garbage collection can discard vector tables or retained symbols unless the linker script keeps them.
- Shrinking a stack based on a test that never hit the deepest path causes field crashes.
- DMA buffers may be restricted to particular RAM regions.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Both regions fit with a stated margin, stack high water marks are measured under load, and the build enforces the limit.
