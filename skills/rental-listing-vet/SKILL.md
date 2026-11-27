---
name: rental-listing-vet
version: 1.0.0
description: >
  Check a holiday let or long-term rental listing and its payment request for fraud signs before any money moves. Use before booking or paying a deposit on a place.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - travel
  - scam
kind: native
status: discovered
tools:
  - read
  - write
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: rental-listing-vet
  official: true
  domain: personal
  security_flags: []
---

# Rental Listing Vet

## When to use
Someone is about to pay for accommodation they have not seen.

## Steps
1. Record the listing URL, host name, address, price, and every message asking for money.
2. Search the address and description text to find the same property under other names or prices.
3. Confirm the place exists using maps, and whether the interior photos fit the building described.
4. Compare price with similar listings. Far below market is a warning, not a bargain.
5. Check how payment is requested. Moving off the booking platform, bank transfer to a person, gift cards, crypto or wire services before viewing are serious red flags.
6. For long-term rentals, require a viewing in person or by trusted proxy, proof the person may let it, a written agreement, and any legally required deposit protection.
7. Test the contact: ask a specific question about the property and ask to verify identity through the platform or a registered agent's independently found number.
8. Report the findings as signs seen and checks that could not be done, with a clear advice not to pay while red flags are open.

## Watch out for
- Cloned booking sites with near-identical addresses; type the address yourself.
- Urgency such as many others waiting or an owner abroad who will post keys.
- Good reviews alone prove little.
- If money was already sent, tell them to contact their bank immediately and report it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each check is marked passed, failed or unverifiable, and no payment step is suggested while a serious flag is unresolved.
