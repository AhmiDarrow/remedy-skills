---
name: ts-esm-cjs-interop-fix
version: 1.0.0
description: >
  Fix ES module versus CommonJS failures in Node and TypeScript projects. Use when you hit ERR_REQUIRE_ESM, cannot use import statement, or default imports that come back undefined.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - typescript
  - nodejs
  - build
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: ts-esm-cjs-interop-fix
  official: true
  domain: tooling
  security_flags: []
---

# Ts Esm Cjs Interop Fix

## When to use
Code type-checks but fails at runtime on import, or a dependency upgrade turned it ESM-only.
## Steps
1. Collect the facts: `node --version`, the nearest `package.json` `type` field, the file extension of the failing file, and `module`, `moduleResolution` and `esModuleInterop` in `tsconfig.json`. Use `tsc --showConfig` to see inherited values.
2. Open the emitted JavaScript that Node actually runs. It tells you whether TypeScript produced `require` or `import`.
3. Decide the project's runtime format. For Node execution use `module` set to `nodenext`; for bundled apps use `moduleResolution` set to `bundler`. Do not mix their assumptions.
4. In Node ESM, add file extensions to relative imports (`./util.js`, even from a `.ts` source) and replace `__dirname` with a path derived from `import.meta.url`.
5. For an ESM-only dependency used from CommonJS, use `await import()` and make sure the compiler is not rewriting it to `require`. Newer Node releases can `require` some ESM modules without top-level await; check the installed version before relying on it.
6. For undefined default imports, log the namespace object to see its real shape, then fix the import form. Do not stack `.default.default`.
7. Inspect the dependency's `exports` map: deep imports not listed there fail even if the file exists.
8. Verify with the plain `node` command used in production, not only a test runner or dev loader.
## Watch out for
- Test runners and loaders transpile differently and can hide a failure that production Node will hit.
- Publishing both formats can load two copies of a package, breaking `instanceof` and singletons.
- Pinning the old CommonJS release is a valid stopgap only if it still receives fixes; note it.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The built output starts under the production Node command with no module errors, and the chosen format is consistent across `package.json` and `tsconfig.json`.
