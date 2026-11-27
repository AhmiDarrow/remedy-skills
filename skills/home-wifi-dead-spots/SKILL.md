---
name: home-wifi-dead-spots
version: 1.0.0
description: >
  Find why home Wi-Fi is slow or drops in some rooms by measuring before buying anything. Use when there are weak signal areas, buffering or video calls that cut out.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - tech-help
  - network
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: home-wifi-dead-spots
  official: true
  domain: personal
  security_flags: []
---

# Home Wifi Dead Spots

## When to use
Home internet is poor in places or at times.

## Steps
1. Ask where, when, which devices and whether wired devices suffer too.
2. Test wired next to the router several times. If that is also slow or dropping, the problem is the line, modem or provider; collect timed results for them.
3. Test on the same device by Wi-Fi beside the router, then in each problem room. Record signal strength and speed in a table.
4. On the computer, read link details: Windows `netsh wlan show interfaces` in PowerShell or cmd (recent Windows 11 may refuse until Location services are allowed; ask before changing that setting); Linux `iw dev` for the interface name, then `iw dev NAME link`; on macOS hold Option and click the Wi-Fi icon.
5. Check for a ping problem: ping the router's address and a public host at the same time during a drop. Loss to the router means the local link.
6. Try free fixes first: central, raised, open router position away from metal and thick walls; compare bands, since higher ones are faster but reach less; try a less crowded channel; check for firmware updates.
7. Only then consider a wired access point, mesh with good backhaul or powerline, matched to where the measurements fall off. Retest after each change.

## Watch out for
- A repeater placed inside the dead spot has nothing good to repeat; it belongs where signal is still strong.
- Two routers both doing address assignment on one network.
- Comparing speed tests from different devices.
- A factory reset can erase provider settings; save them first.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Before and after measurements by room show the fault located and improved, or evidence is ready for the provider.
