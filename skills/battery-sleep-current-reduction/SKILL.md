---
name: battery-sleep-current-reduction
version: 1.0.0
description: >
  Reduce power draw in a battery-powered microcontroller device by measuring sleep current and wake energy. Use when battery life falls far short of the estimate.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - embedded
  - hardware
  - power
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - write
metadata:
  source: library
  library_id: battery-sleep-current-reduction
  official: true
  domain: tooling
  security_flags: []
---

# Battery Sleep Current Reduction

## When to use
Firmware and board draw more than the design budget. The user performs electrical measurements.
## Steps
1. Write an energy budget: each state's current times its duration per cycle, plus battery self-discharge and derating for temperature and cutoff voltage.
2. Set up measurement that captures both microamp sleep and short high peaks, ideally a power analyzer. A multimeter's auto range can brown out the board or miss bursts.
3. Disconnect the debugger and power-cycle before measuring; debug logic can keep clocks running.
4. Measure a minimal firmware that only enters the deepest intended sleep mode. This is the board floor.
5. If the floor is high, account for regulator quiescent current, power LEDs, USB serial chips, pull resistors across driven lines and sensor modules. Isolate one at a time following the board design.
6. Configure unused pins per the datasheet, and avoid floating inputs.
7. Before sleeping, put external parts into their low-power modes, stop unused clocks and peripherals, and check no pin back-powers an unpowered chip.
8. Shorten awake time: replace delays and polling with interrupts, and batch radio transmissions.
9. Log wake reasons and counts to catch spurious wakeups.
10. Recalculate battery life from measured values.
## Watch out for
- Development boards often cannot reach the chip datasheet figure.
- Deep sleep may lose RAM or require clock reinitialization on wake.
- Coin cells sag on radio peaks; check minimum voltage, not only average current.
- Keep a recovery route for reflashing if firmware sleeps immediately at boot.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Measured sleep current and per-wake energy are recorded, and the recalculated lifetime meets the budget or the remaining gap is attributed to named components.
