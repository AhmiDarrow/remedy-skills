---
name: ups-shutdown-setup
version: 1.0.0
description: >
  Configure a UPS so servers and storage shut down cleanly during power cuts and come back correctly, using monitoring such as NUT. Use when adding or checking battery backup for a server or homelab.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - homelab
  - power
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
  - owner.notify
metadata:
  source: library
  library_id: ups-shutdown-setup
  official: true
  domain: ops
  security_flags: []
---

# Ups Shutdown Setup

## When to use
A UPS protects computers but nothing has proven they will shut down before the battery empties.

## Steps
1. List what is plugged into battery outlets with measured load, including router, switches and storage. Leave high-draw devices such as laser printers off.
2. Check runtime at that load from the UPS or its vendor chart, allowing for battery ageing.
3. Connect by USB or network and detect it with a supported driver, for example with Network UPS Tools. Verify readings with `upsc <name>`.
4. Make one host the server for UPS state and the others clients over the network with limited accounts.
5. Time a real shutdown of each system, including VMs and storage.
6. Set the shutdown trigger by time on battery or remaining charge with generous margin over that duration.
7. Order shutdown: dependants and VMs first, storage later, the UPS monitoring host last. Keep networking powered long enough to signal clients.
8. Configure return behaviour: firmware "restore on AC power" settings and start order. Handle power returning in the middle of a shutdown.
9. Add notifications for on-battery, low battery, communication lost and replace-battery.
10. In an agreed window with backups verified, simulate forced shutdown, then pull input power for a short supervised test.

## Watch out for
- A simulated forced shutdown really shuts systems down and may cut UPS output.
- If the UPS keeps supplying power after hosts halt and mains returns, they may never see a power cycle and stay off.
- Some computer power supplies behave badly on stepped-approximation output.
- A battery reporting full charge can still fail under load.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A supervised power test shows alerts, ordered clean shutdown with margin, and correct restart, with measured runtime recorded.
