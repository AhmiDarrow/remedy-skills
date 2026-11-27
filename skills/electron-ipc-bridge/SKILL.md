---
name: electron-ipc-bridge
version: 1.0.0
description: >
  Design a safe, typed bridge between an Electron renderer and main process with preload, validation and hardening. Use when adding native features or reviewing Node access from web content.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - desktop
  - electron
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: electron-ipc-bridge
  official: true
  domain: frontend
  security_flags: []
---

# Electron Ipc Bridge

## When to use
An Electron app exposes `ipcRenderer` directly, enables Node integration, or needs new file or system access from the UI.

## Steps
1. Read every `BrowserWindow` and web view setting and the Electron version. Target `contextIsolation: true`, `sandbox: true` and `nodeIntegration: false`.
2. `grep` for `ipcMain`, `ipcRenderer`, `exposeInMainWorld`, `shell.openExternal` and remote-module use.
3. In preload expose one narrow function per capability through `contextBridge`, such as `saveReport(data)`, never generic `send`, `invoke` or arbitrary channel names.
4. Use `invoke` with `ipcMain.handle` for request and response. For events, wrap the callback so the raw event object is not handed to the page, and return an unsubscribe function.
5. In every handler validate the sender frame's origin and the argument types, sizes and ranges.
6. Do not accept arbitrary paths or commands. Let the main process show the file dialog, or resolve names within an allowed directory and reject escapes after normalisation.
7. Allowlist protocols and hosts before `openExternal`; restrict navigation and new windows with `will-navigate` and `setWindowOpenHandler`.
8. Set a Content Security Policy and load app content from local or a custom protocol rather than remote pages with privileges.
9. Keep one shared type definition for the bridge, and test rejected inputs.

## Watch out for
- Context isolation does not help if preload exposes a function that can do anything.
- TypeScript types are not run-time validation.
- Values crossing IPC are copied; functions and class behaviour do not survive.
- Synchronous IPC freezes the renderer.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Window settings match the targets or each exception is justified, no generic channel is exposed, and tests show bad senders, paths and URLs are rejected.
