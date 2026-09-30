# definable

[![npm version](https://img.shields.io/npm/v/%40johnhenry%2Fdefinable.svg)](https://www.npmjs.com/package/@johnhenry/definable)
[![CI](https://github.com/johnhenry/definable/actions/workflows/ci.yml/badge.svg)](https://github.com/johnhenry/definable/actions/workflows/ci.yml)
[![license](https://img.shields.io/npm/l/%40johnhenry%2Fdefinable.svg)](LICENSE)

Full documentation: [opensource.johnhenry.me/definable](https://opensource.johnhenry.me/definable/)

> **Archived.** This package is folded back into
> [`@johnhenry/domkit`](https://github.com/johnhenry/domkit) as of domkit
> `0.0.4` — import `@johnhenry/domkit/definable/<module>/...` instead. The
> unscoped npm package `@johnhenry/definable` is deprecated (not removed)
> and will keep working at its last published version; this repo is
> archived (read-only, not deleted).

> **Provenance:** extracted from [`johnhenry/lib`](https://github.com/johnhenry/lib)'s
> `js/` directory. Briefly part of [`@johnhenry/domkit`](https://github.com/johnhenry/domkit)
> (a toolkit of ~40 independent DOM/HTML-component modules), then split out
> as its own package because this cluster has a real internal shape of its
> own -- four ways of getting behavior onto a page declaratively, from four
> different kinds of source.

Five small modules for declaratively loading or defining custom elements
and globals, without writing a `customElements.define(...)` call by hand:

| Module | What it does |
|---|---|
| [`definetag`](src/definetag/readme.md) | Curried `customElements.define` wrapper: `(elementClass) => (name) => ...`. The low-level primitive the others build on. |
| [`define-component.component`](src/define-component.component/readme.md) | `<define-component name="x" src="./x.mjs">` -- dynamically imports a module by URL and registers its export as a custom element. |
| [`define-component-by-content.component`](src/define-component-by-content.component/readme.md) | `<define-component-by-content name="x" content="<p>Hi</p>">` -- defines a custom element from an inline HTML string instead of a separate module file. Built on [`@johnhenry/domable`](https://github.com/johnhenry/domable)'s `simple-element`. |
| [`polyfill-window.component`](src/polyfill-window.component/readme.md) | `<polyfill-window name="x" src="./x.mjs">` -- the same URL-loading idea as `define-component`, but assigns the import to a `globalThis` key instead of registering a custom element. |
| [`until-window-load`](src/until-window-load/readme.md) | Declarative "remove this loading class once `window` has loaded" helper -- used by `polyfill-window.component`'s own demo to avoid a flash of unstyled content. |

## Install

```sh
npm install @johnhenry/definable
```

```js
import definetag from "@johnhenry/definable/definetag/index.mjs";
```

or, in a browser with no build step, via a CDN:

```html
<script
  type="module"
  src="https://esm.sh/@johnhenry/definable/define-component.component/global.mjs"
></script>
<define-component name="my-widget" src="./my-widget.mjs"></define-component>
<my-widget></my-widget>
```

## Which one do I want?

| I have... | Use |
|---|---|
| A module file (default or named export is a custom-element class) | `define-component.component` |
| A small HTML string I want to become a tag | `define-component-by-content.component` |
| A module whose export should just be a global, not a tag | `polyfill-window.component` |
| My own class already, just need to register it under a name | `definetag` directly |

## Family

- [`@johnhenry/domable`](https://github.com/johnhenry/domable) -- `define-component-by-content.component`
  depends on its `simple-element` `constructSuperclass` for building the
  actual custom-element class from an HTML string.
- [`@johnhenry/domkit`](https://github.com/johnhenry/domkit) -- the toolkit
  this package was originally part of. Several of its still-resident
  modules (`animate-paths.component`, `chernoff-face`, `xy-grapher`) depend
  on `definable` (`definetag`, `define-component.component`) to register
  themselves.
- [`@johnhenry/respondable`](https://github.com/johnhenry/respondable) --
  `query-container.component`'s own demo bootstraps via this package's
  `define-component.component`.

## License

MIT
