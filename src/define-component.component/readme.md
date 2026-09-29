# Define Component

Dynamically loads a module by URL and registers its export as a custom
element — the generic "define a component from a URL" pattern referenced
by [polyfill-window.component](../polyfill-window.component/readme.md)'s
own demo, and by [`@johnhenry/respondable`](https://github.com/johnhenry/respondable)'s
`query-container.component` and [`@johnhenry/domkit`](https://github.com/johnhenry/domkit)'s
`animate-paths.component`, both of which bootstrap via this exact pattern.

Compare [define-component-by-content.component](../define-component-by-content.component/readme.md),
which defines a component from an inline HTML string instead of a separate
module file.

## Attributes

| Attribute | Description |
|---|---|
| `name` | Tag name to register (required) |
| `src` | URL of the module to import, resolved relative to the current document (required) |
| `import` | Named export to use as the element class. Defaults to the module's default export |
| `force` | If present, re-imports and re-registers even if `name` is already a registered custom element |

## Usage

```html
<script
  type="module"
  src="https://esm.sh/@johnhenry/definable/define-component.component/global.mjs"
></script>
<define-component name="my-widget" src="./my-widget.mjs"></define-component>
<my-widget></my-widget>
```
