---
name: inventory-reorder-point
version: 1.0.0
description: >
  Set reorder points and order quantities from sales history, supplier lead times and safety stock. Use when a shop keeps running out of items or tying cash up in surplus.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - small-business
  - inventory
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: inventory-reorder-point
  official: true
  domain: data
  security_flags: []
---

# Inventory Reorder Point

## When to use
Stock is reordered by feel.

## Steps
1. Gather per item: sales by day or week, current stock, open orders, backorders, lead times actually observed, pack size, minimum order, shelf life.
2. Reconcile system stock with a physical count for important items.
3. Remove or flag weeks when the item was out of stock, since sales then understate demand.
4. Separate steady, seasonal, intermittent and new items.
5. Reorder point = average daily demand * lead time days + safety stock.
6. For a simple safety stock use high-case demand over high-case lead time minus the average, and label the method; check it against past stockouts.
7. Compare against inventory position: on hand + on order - committed.
8. Round quantities to pack sizes and check cash, space and expiry. Replay past data, then review on a schedule. The user places orders.

## Watch out for
- Mixing weekly demand with lead time in days.
- Using quoted instead of actual lead times.
- Applying averages to items that sell rarely or seasonally.
- Reordering again because stock on order was ignored.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each priority item has inputs, reorder point and quantity with units, and exceptions needing judgment are listed.
