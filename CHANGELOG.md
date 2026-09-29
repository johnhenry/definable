# Changelog

All notable changes to this project will be documented in this file.

## [0.0.0] - 2026-09-29

Initial release. Extracted from [`@johnhenry/domkit`](https://github.com/johnhenry/domkit)
(originally from [`johnhenry/lib`](https://github.com/johnhenry/lib)'s `js/`
directory) -- the "define a component declaratively" module family
(`definetag`, `define-component.component`, `define-component-by-content.component`,
`polyfill-window.component`), split into its own package because it has a
real internal shape (four related ways to get behavior onto a page from
four different kinds of source), distinct from domkit's grab-bag of
unrelated widgets.

- `definetag`, `define-component.component`, `define-component-by-content.component`,
  `polyfill-window.component` moved in unchanged (all four already had
  accurate READMEs from domkit's own consolidation pass).
- `define-component-by-content.component` continues to depend on
  `@johnhenry/domable`'s `simple-element` `constructSuperclass`, same as it
  did inside domkit.
- Added `until-window-load` -- a module `polyfill-window.component`'s own
  `demo.html` has always referenced (`../until-window-load/index.mjs`) but
  that was never actually migrated out of `lib` during domkit's original
  extraction, leaving a dangling import in that demo the whole time. Found
  while porting the demo here; copied in from `lib`'s `js/until-window-load/0.0.0/`
  and its README's stale absolute `johnhenry.github.io/lib` URLs (and a
  `remove-loading-classes` vs. `until-window-load` naming inconsistency)
  fixed at the same time.
- Domkit's copies of these four original modules were removed; nothing
  else in domkit imported them except `animate-paths.component`,
  `chernoff-face`, and `xy-grapher`, which now depend on
  `@johnhenry/definable` instead of a local relative import.
