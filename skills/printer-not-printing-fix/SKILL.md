---
name: printer-not-printing-fix
version: 1.0.0
description: >
  Diagnose a home printer that is offline, stuck or printing badly by isolating printer, network, queue and driver. Use when a document will not print.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - tech-help
  - printing
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: printer-not-printing-fix
  official: true
  domain: personal
  security_flags: []
---

# Printer Not Printing Fix

## When to use
A home or small office printer has stopped working from one or all devices.

## Steps
1. Get printer model, computer system, connection type, exact message and what last changed.
2. Read the printer's own screen and print its built-in test or status page. If that fails or looks bad, work on paper, ink or toner and hardware, not the computer.
3. Check whether any other device can print. That splits printer or network from one machine.
4. For network printers, print the network status page, confirm the printer is on the same network as the computer (not a guest network) and ping its address.
5. Check the right queue is selected and not paused; old duplicate queues are common. Clear the user's stuck jobs after they agree. On Windows, `Get-Printer` and `Get-PrintJob -PrinterName NAME` in PowerShell show state; on macOS or Linux, `lpstat -p -o`.
6. If the address changed after a router restart, reserve it in the router or re-add the printer.
7. Re-add the printer using the system's built-in driverless option or the maker's driver from its official site.
8. For faint or streaked output, use the printer's own alignment and cleaning routine sparingly.

## Watch out for
- Fake "printer support" pages and phone numbers in search results; get drivers only from the maker or the operating system.
- Ask before restarting the spooler or deleting queues on a work computer.
- Repeated cleaning cycles use a lot of ink.
- Pulling jammed paper against the paper path or leaving torn scraps.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A test page prints from the affected device, or the fault is isolated to the printer with its symptoms recorded.
