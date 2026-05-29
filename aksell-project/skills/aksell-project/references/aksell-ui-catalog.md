# @aksell/ui Component Catalog

CDN base: `https://unpkg.com/@aksell/ui/src/`

---

## Stylesheets

| File | Purpose | Auto-loaded in html template? |
|------|---------|-------------------------------|
| `styles/resets.css` | Browser resets | ✅ Yes |
| `styles/colors.css` | Brand color CSS custom properties | ✅ Yes |
| `styles/typography.css` | Font scale, headings, body text | ✅ Yes |
| `styles/btn.css` | Button classes | ✅ Yes |
| `styles/native.css` | Native HTML element styles (inputs, selects, tables, etc.) | ❌ Add manually |
| `styles/utilities.css` | Spacing and display helpers | ❌ Add manually |
| `styles/components/toast.css` | Toast notification styles | ❌ Add manually |
| `styles/components/pillarrowbtn.css` | PillArrowBtn styles (not needed if using standalone.js) | ❌ Add manually |

---

## Native HTML Elements (styled by native.css)

These work out of the box once `native.css` is loaded. No extra classes needed.

- `<input type="text">`, `type="search"`, `type="number"`, `type="email"`, `type="tel"`, `type="password"`, `type="date"`, `type="time"`
- `<textarea>`
- `<select>` / `<option>`
- `<label>` / `<fieldset>` / `<legend>`
- `<table>` / `<thead>` / `<tbody>` / `<tr>` / `<th>` / `<td>`
- `<details>` / `<summary>`
- `<input type="checkbox">`, `type="radio"` (incl. `role="switch"` for toggles)
- `<input type="range">`
- `<input type="reset">`, `type="submit"` (also button-styled)

Always pair inputs with `<label>` elements.

---

## Buttons (btn.css)

Base class required: `btn`

Modifiers:
- `btn--primary` — main CTA
- `btn--success` — confirm/save actions
- `btn--warning` — caution actions
- `btn--danger` — destructive actions

```html
<button class="btn btn--primary">Save</button>
<button class="btn btn--danger">Delete</button>
```

Group buttons:
```html
<div class="btn-row">
  <button class="btn btn--primary">Submit</button>
  <button class="btn">Cancel</button>
</div>
```

---

## Toast (JS component)

Link CSS and import JS:
```html
<link rel="stylesheet" href="https://unpkg.com/@aksell/ui/src/styles/components/toast.css" />
```
```js
import 'https://unpkg.com/@aksell/ui/src/components/Toast/standalone/toast.standalone.js';
```

Usage — dispatch a CustomEvent on `document`:
```js
document.dispatchEvent(new CustomEvent('aksell:toast', {
  detail: { message: 'Copied!', type: 'success' } // type: 'success' | 'error' | 'info' | 'warning'
}));
```

The toast component listens for `aksell:toast` events and renders them automatically.
No HTML markup required beyond loading the component.

---

## PillArrowBtn (JS web component)

CSS is bundled in the standalone JS — no separate link needed:
```js
import 'https://unpkg.com/@aksell/ui/src/components/PillArrowBtn/standalone/PillArrowBtn.standalone.js';
```

Usage:
```html
<pill-arrow-btn href="/path">Label</pill-arrow-btn>
```

---

## Colors (CSS custom properties from colors.css)

Use via `var(--color-*)`. Check `colors.css` source for full list.
Common: `--color-brand`, `--color-text`, `--color-bg`, `--color-border`

---

## What NOT to Do

- Don't add `node_modules` or run `npm install` in the html template
- Don't copy CSS from `@aksell/ui` into the project
- Don't add Tailwind, Bootstrap, or other utility frameworks
- Don't add a bundler (Vite, Webpack, etc.) unless the user requests it
- Don't add the Aeonik font unless the project has a valid license
