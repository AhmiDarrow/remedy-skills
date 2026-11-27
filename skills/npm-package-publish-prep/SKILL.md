---
name: npm-package-publish-prep
version: 1.0.0
description: >
  Check an npm library's contents, entry points, types and version before release. Use before publishing a package or when consumers report missing files or types.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - javascript
  - npm
  - release
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
  - grep
metadata:
  source: library
  library_id: npm-package-publish-prep
  official: true
  domain: tooling
  security_flags: []
---

# Npm Package Publish Prep

## When to use
Preparing a first or new release of a JavaScript or TypeScript library. Publishing itself needs the owner's go-ahead.
## Steps
1. Run `npm pack --dry-run` and read the file list. Look for tests, fixtures, local config, `.env` files and source maps that embed private paths, and for missing build output.
2. Restrict contents with the `files` allow list in `package.json` instead of relying on ignore files.
3. Verify every path in `exports`, `main`, `bin` and `types` exists inside the tarball. In conditional exports, `types` must come first and `default` last.
4. Confirm runtime imports are all in `dependencies`; anything only in `devDependencies` will be missing for users. Host frameworks belong in `peerDependencies`.
5. Create the real tarball with `npm pack`, install it into an empty scratch project, and both import it (ESM, and require if you claim support) and type-check a small consumer file.
6. For CLIs, check the bin file starts with `#!/usr/bin/env node` and runs from the installed location.
7. Set `engines` to versions you actually test.
8. Pick the version from the change set, mark prereleases with a dist-tag such as `--tag next`, and show the owner the tarball list and version before `npm publish`.
## Watch out for
- A published version number can never be reused, even after unpublishing, and unpublishing is restricted. Verify before, not after.
- npm 11 and later refuse to publish a prerelease without `--tag`; older versions and some other clients mark it `latest`. Always set the tag explicitly.
- Scoped packages default to restricted access; a public one needs `--access public`.
- Testing through a workspace link hides missing files, because the whole source folder is visible.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The packed tarball installs and works in an empty project, its file list contains no secrets or stray files, and the owner has approved the version.
