---
name: web-component-authoring
version: 1.0.0
description: >
  Build a framework-independent custom element with sound attributes, events, styling hooks and form participation. Use when a widget must work across several frameworks or in plain HTML.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - web-components
  - components
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
  - computer.navigate
  - computer.snapshot
metadata:
  source: library
  library_id: web-component-authoring
  official: true
  domain: frontend
  security_flags: []
---

# Web Component Authoring

## When to use
A control has to be shared by apps on different stacks, or an existing custom element misbehaves inside forms or frameworks.

## Steps
1. Write the public contract first: tag name with a hyphen, attributes, properties, events, slots, CSS custom properties and parts.
2. Do setup that depends on attributes or children in `connectedCallback`, not the constructor. Make it safe to run twice, because moving an element reconnects it. Remove outside listeners in `disconnectedCallback`.
3. Reflect only primitive values between attributes and properties. List watched names in `static observedAttributes` and guard against reflection loops.
4. Upgrade early properties: if a framework set `el.value` before definition, save the own property, delete it, and reassign it through the setter.
5. Dispatch `CustomEvent`s with `bubbles: true` and, when they must leave shadow roots, `composed: true`. Put data in `detail`.
6. Expose styling through custom properties and `part` attributes, and define `:host([hidden]) { display: none }`.
7. For form controls set `static formAssociated = true`, use `attachInternals()`, call `setFormValue` and `setValidity`, and implement reset callbacks.
8. Use native elements inside the shadow root where possible. Check labelling and focus; `delegatesFocus` helps composite controls.
9. Test in a plain HTML page first, then in each consuming framework.

## Watch out for
- ID references such as `aria-labelledby` and `label for` do not cross shadow boundaries.
- Calling `customElements.define` twice for one name throws, which happens when two bundles ship the element.
- Server rendering shows an undefined element until script loads; style `:not(:defined)` to avoid a flash.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The element works from plain HTML with keyboard and screen reader labelling, submits and resets in a native form if it is a control, and every contract item is exercised in a demo page.
