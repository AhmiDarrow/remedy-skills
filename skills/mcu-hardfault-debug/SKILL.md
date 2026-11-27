---
name: mcu-hardfault-debug
version: 1.0.0
description: >
  Decode a hard fault or unexplained reset on an ARM Cortex-M microcontroller to the offending instruction. Use when firmware locks up, lands in HardFault_Handler or reboots randomly.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - embedded
  - firmware
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
  library_id: mcu-hardfault-debug
  official: true
  domain: tooling
  security_flags: []
---

# Mcu Hardfault Debug

## When to use
Embedded firmware crashes. For other architectures, use the same method with that core's fault registers from its manual.
## Steps
1. Establish the core (M0, M3, M4, M7, M33) from the part number; fault status detail differs, and M0-class parts have little of it.
2. Read the reset cause register early in startup and log it, to separate fault, watchdog, brown-out and external reset. Clear flags after reading.
3. Add a fault handler that selects MSP or PSP from the EXC_RETURN value and captures the stacked R0-R3, R12, LR, PC and xPSR into RAM that survives reset.
4. On M3 and above also capture CFSR, HFSR, MMFAR and BFAR. Use the address registers only when their valid bits are set.
5. Map the stacked PC and LR to source with `arm-none-eabi-addr2line -e firmware.elf <addr>` using the exact ELF that was flashed.
6. Interpret: precise bus errors point at the instruction; imprecise ones happened earlier, often on a buffered write; undefined instruction or bad state suggests a corrupt function pointer.
7. Check stack overflow with watermark patterns or stack limit features, and check unaligned access where the core faults on it.
8. Verify the suspect peripheral's clock is enabled before register access.
9. Reproduce with a watchpoint on the corrupted address, then fix and run the trigger repeatedly.
## Watch out for
- A watchdog reset can look like a random crash.
- The debugger may change timing, keep clocks on or halt the watchdog.
- Printing from the fault handler over interrupt-driven UART will hang.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The faulting source line and the reason for the bad address or instruction are shown from captured registers, or the reset is proven to have another cause.
