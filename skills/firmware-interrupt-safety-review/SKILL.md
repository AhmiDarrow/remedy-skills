---
name: firmware-interrupt-safety-review
version: 1.0.0
description: >
  Review embedded firmware for races between interrupts, tasks and DMA. Use when values corrupt rarely, an interrupt-driven driver stalls, or behavior changes with optimization level.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - embedded
  - firmware
  - concurrency
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: firmware-interrupt-safety-review
  official: true
  domain: tooling
  security_flags: []
---

# Firmware Interrupt Safety Review

## When to use
Bare-metal or RTOS firmware shares data between execution contexts.
## Steps
1. List every interrupt handler with its priority, then every variable, buffer and peripheral register also touched outside it.
2. Mark shared accesses that are not single and atomic on this core: multi-word values, read-modify-write, bit fields and head and tail pairs.
3. Protect them with the narrowest tool: C11 atomics where supported, a short critical section that saves and restores the previous interrupt state, or a single-producer single-consumer queue with correct ordering.
4. Use `volatile` for hardware registers and simple flags only; it gives neither atomicity nor ordering of other data.
5. In RTOS code, call only the interrupt-safe API variants and check the interrupt's priority is within the range allowed to call them. Check the port's priority numbering direction.
6. Keep handlers short: no blocking, allocation or lengthy printing. Defer work to a task or main loop.
7. Verify each handler clears its flag the way the reference manual requires, early enough to avoid immediate re-entry.
8. For DMA, ensure the buffer is not touched while owned by hardware, is not on a returned stack frame, and on cached cores gets clean or invalidate operations with proper alignment.
9. Close the sleep race where an event arrives between checking the flag and sleeping, using the core's recommended sequence.
10. Stress with maximum interrupt rates and optimization enabled.
## Watch out for
- Unconditionally re-enabling interrupts at the end of a critical section breaks nested use.
- Shared peripheral buses need ownership, not only variable protection.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every shared item has a named protection mechanism, and the stress run on hardware shows no corruption or stalls.
