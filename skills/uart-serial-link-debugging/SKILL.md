---
name: uart-serial-link-debugging
version: 1.0.0
description: >
  Diagnose serial links that print garbage, drop bytes or stay silent between boards and computers. Use when bringing up a UART console or a serial protocol on embedded hardware.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - embedded
  - hardware
  - serial
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: uart-serial-link-debugging
  official: true
  domain: tooling
  security_flags: []
---

# Uart Serial Link Debugging

## When to use
A UART or USB serial connection does not carry data correctly.
## Steps
1. Identify the electrical standard on both ends: logic-level 3.3 V or 5 V, RS-232 or RS-485. Do not connect RS-232 voltages to logic pins.
2. Confirm TX goes to RX both ways and grounds are joined.
3. Identify the right port (`dmesg` and `/dev/serial/by-id` on Linux, Device Manager on Windows) and that no other program holds it.
4. Match baud rate, data bits, parity, stop bits and flow control.
5. Test each side alone with a loopback of TX to RX.
6. For garbage, compute the real baud rate from the configured peripheral clock and divider; a wrong clock tree is common. Send `0x55` and measure the bit time on a scope.
7. For lost bytes, check overrun and framing error flags, then use interrupt or DMA reception with a ring buffer, idle-line detection and a counter for overflow.
8. For binary protocols, add framing with length or delimiters, a checksum and resynchronization after corruption. One read call is not one message.
9. Account for open-port side effects: some boards reset when DTR toggles, so the first bytes are lost.
10. Run a long transfer with sequence numbers in both directions and count errors.
## Watch out for
- Text mode or newline translation on the host corrupts binary data.
- RS-485 half duplex needs the driver enable released only after the last bit has left, not when the buffer empties.
- Debug prints from an interrupt handler cause the very overruns being investigated.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The sequence-numbered soak test at the working baud rate completes with zero unexplained losses, and settings for both ends are recorded.
