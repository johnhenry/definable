# Agent playbook

`@johnhenry/definable` -- five small modules for declaratively loading or
defining custom elements/globals (from a URL, from inline HTML content, or
as a plain global polyfill), plus the curried `customElements.define`
primitive (`definetag`) they're built on. One npm package, one subpath
export per module (`"./*": "./src/*"`) -- no shared barrel, no build step.

`CLAUDE.md` in this directory is a symlink to this file.

## The verification loop (before every push)

1. `node --check` every `.mjs`/`.js` file you touched.
2. No DOM test environment is configured -- verify a DOM-touching change
   against the module's own `demo.html` in a real browser
   (`npx serve .` from the repo root, then open `src/<module>/demo.html`).
3. `npm pack --dry-run` -- confirm the file list is complete.
4. A genuinely fresh clone: `git clone . /tmp/definable-verifyN && cd $_ && npm ci && npm test`.

## Repo-specific gotchas

- **`define-component-by-content.component` depends on `@johnhenry/domable`**
  (`import { constructSuperclass } from "@johnhenry/domable/simple-element"`)
  -- a real npm dependency, not a local copy. If you're comparing against
  an old `lib`/`domkit` copy of this file, remember it used to import
  `simple-element` via a relative sibling path; it doesn't anymore.
- **`until-window-load` was a genuinely missing module** until this
  package's `0.0.0` release -- `polyfill-window.component`'s `demo.html`
  referenced it the whole time it lived in `domkit`, but it was never
  actually migrated out of `lib` during domkit's original extraction. If
  you find another dangling reference like this while touching a demo
  file, check `~/Projects/lib/js/` (or the equivalent) before assuming the
  target doesn't exist anywhere.
- **`animate-paths.component`, `chernoff-face`, and `xy-grapher` still live
  in `@johnhenry/domkit`** and depend on this package (`definetag`,
  `define-component.component`) to register themselves. A breaking change
  to either of those two modules' public shape needs a coordinated bump
  on domkit's side too.

## Definition of done (adding or changing a module)

- `node --check` passes.
- The module's own `readme.md` is accurate (name, description, real
  attributes/API, a working usage example).
- Any cross-package reference (to `@johnhenry/domable`, `@johnhenry/domkit`,
  `@johnhenry/respondable`) in a README or demo file uses the real published
  package name, not a stale relative path from when this was still inside
  domkit.

## Non-goals

- No bundling/build step is planned -- modules ship as source.
- No test environment (jsdom/happy-dom) exists yet, matching domkit's own
  current state.

## Releases

Bump `version` in `package.json` in a PR, add a `CHANGELOG.md` entry,
merge, then `gh release create v<version>` (fires
`.github/workflows/publish.yml`, gated on the full CI suite).
