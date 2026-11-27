---
name: smart-home-automation-design
version: 1.0.0
description: >
  Design a home automation that behaves sensibly when sensors fail, people override it or the internet drops. Use when creating or fixing smart home routines.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - smart-home
  - automation
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: smart-home-automation-design
  official: true
  domain: personal
  security_flags: []
---

# Smart Home Automation Design

## When to use
Someone wants lights, heating, sensors or alerts to act automatically.

## Steps
1. State the outcome and who lives there, including guests, children, pets and people who will not use an app.
2. List devices, hub and what runs locally versus through a cloud service.
3. Write the rule as trigger, conditions, action and ending. Every "turn on" needs a defined way back off.
4. Decide manual override: wall switches must still work, and say how long an automation stays off after someone overrides it.
5. Walk through failures: dead battery, stale sensor reading, offline hub, power restored, nobody's phone home, two rules fighting. Pick the safe default for each.
6. Add delays and separate on and off thresholds so values hovering at a limit do not cause flapping.
7. Keep safety functions on certified standalone devices. Automations may add alerts but never replace smoke or CO alarms, and heaters, ovens and locks should not act unattended without a deliberate decision.
8. Test each branch by forcing the trigger, then observe logs for a few days.

## Watch out for
- Motion-only lights switching off on someone sitting still.
- Phone location as the sole presence signal.
- Auto-unlock triggered by a drifting location.
- Alerts so frequent they get muted.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each rule has on, off, override and failure behaviour written down and its branches tested.
