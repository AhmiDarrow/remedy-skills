---
name: i2c-bus-debugging
version: 1.0.0
description: >
  Debug an I2C sensor or peripheral that does not acknowledge, returns wrong bytes or hangs the bus. Use when bringing up a new device on a microcontroller or single-board computer.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - embedded
  - hardware
  - i2c
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: i2c-bus-debugging
  official: true
  domain: tooling
  security_flags: []
---

# I2C Bus Debugging

## When to use
I2C communication fails or is flaky. The user does the wiring and measurements; you guide and read the code.
## Steps
1. Read the datasheet for supply voltage, logic levels, address, maximum clock, power-up delay and register protocol.
2. Have the user check, with power off while rewiring: common ground, SDA and SCL not swapped, correct supply, and level shifting where voltages differ.
3. With power on and the bus idle, both lines should be high. A low line means missing pull-ups, a short, wrong pin setup or a device holding it.
4. Check pull-ups exist and are not stacked from several breakout boards. Slow rising edges on a scope call for a stronger value within the specification.
5. Scan the bus (`i2cdetect -y <bus>` on Linux, noting that probing can upset some devices; confirm the bus is the right one).
6. Resolve address confusion: datasheets may give the 8-bit form while APIs expect 7-bit, and some APIs expect it shifted.
7. Drop to a low clock, read a fixed ID register, and compare with the datasheet value.
8. Check whether register reads need a repeated start, auto-increment bit, conversion delay or clock stretching support.
9. Capture with a logic analyzer to see ACKs and actual bytes.
10. For a stuck SDA after reset, implement recovery: toggle SCL as an open-drain GPIO (never driven high against another device) up to nine pulses until SDA releases, then send a stop, and add timeouts to every transaction.
## Watch out for
- Applying a higher voltage to a lower-voltage part can destroy it; confirm before connecting.
- Internal pin pull-ups are usually too weak.
- Multi-byte values have a defined byte order and sign width that must be applied.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The ID register reads correctly across repeated trials and resets, and failed transactions time out instead of hanging.
