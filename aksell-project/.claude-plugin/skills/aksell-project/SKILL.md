---
name: aksell-project
description: >
  Guide for starting any new Aksell internal tool or page using aksell-ui.
  Use this skill whenever someone says "new aksell project", "build a tool with aksell",
  "scaffold an aksell app", "create aksell page", or starts building any internal
  web tool at Aksell — even if they don't say "skill" or "aksell-ui" explicitly.
  This skill asks the right planning questions, runs `npx create-aksell`, and
  implements the page using correct aksell-ui elements and patterns. Always use
  this before writing any HTML or touching index.html for Aksell projects.
---

# Aksell Project Skill

You are building an internal Aksell tool or page using the aksell-ui design system.
This skill guides you through project setup and ensures you use the right components.

## Step 1: Ask Planning Questions

Ask these questions **one at a time**. Wait for answers before proceeding.

1. **Project name** (kebab-case, e.g. `price-calculator`) — becomes the folder name
2. **Template** — present these options and explain the trade-off:
   - `html` — zero-build, open `index.html` directly in browser. Best for simple tools, calculators, internal forms, one-page utilities.
   - `astro` — full Astro setup with `npm install` + dev server. Best for multi-page apps, data-heavy dashboards, anything needing components or routing.
   - **Recommend `html` by default** unless the user describes something multi-page or framework-dependent.
3. **What does it do?** — one sentence description of the tool's purpose
4. **Key interactions** — what does the user do with it? (fill a form, see a table, copy output, etc.)

Once you have these answers, proceed. You have everything you need.

## Step 2: Scaffold

Run:
```bash
npx create-aksell --name <name> --template <html|astro>
```

This clones from GitHub (`aksellsor/aksell-ui-template-html` or `aksellsor/aksell-ui-template-astro`)
and patches `{{project-name}}` placeholders.

## Step 3: Understand What's in the Template

**HTML template** sets up:
- `index.html` — already links aksell-ui CDN stylesheets (resets, colors, typography, btn)
- `style.css` — project-specific overrides
- `main.js` — entry point for JS
- `AGENTS.md` — the aksell-ui component reference (READ THIS before implementing)

**Astro template** sets up:
- Standard Astro project with `@aksell/ui` as a package dependency
- Run `npm install && npm run dev` to start

## Step 4: Implement Using Aksell-UI

Read `references/aksell-ui-catalog.md` for the full component and style reference before writing any HTML.

### Core Rules

- **Use native HTML elements** — aksell-ui styles them via `native.css`. No custom component wrapper needed for inputs, selects, labels, etc.
- **Buttons use CSS classes** — `<button class="btn btn--primary">` not a custom element
- **Toast and PillArrowBtn are the only JS components** — import as ES modules if needed
- **Never copy CSS from `@aksell/ui` into the project** — always use CDN links
- **Never add Tailwind, Bootstrap, or other utility frameworks**
- **Never add a bundler** unless the user specifically requests it
- **Don't `npm install`** in the html template — it's CDN only

### Adding Stylesheets

Already in `index.html`: `resets.css`, `colors.css`, `typography.css`, `btn.css`

Add more `<link>` tags as needed:
```html
<link rel="stylesheet" href="https://unpkg.com/@aksell/ui/src/styles/native.css" />
<link rel="stylesheet" href="https://unpkg.com/@aksell/ui/src/styles/utilities.css" />
<link rel="stylesheet" href="https://unpkg.com/@aksell/ui/src/styles/components/toast.css" />
<link rel="stylesheet" href="https://unpkg.com/@aksell/ui/src/styles/components/pillarrowbtn.css" />
```

### Adding JS Components

In `main.js`:
```js
// Toast
import 'https://unpkg.com/@aksell/ui/src/components/Toast/standalone/toast.standalone.js';

// PillArrowBtn (CSS bundled, no separate link needed)
import 'https://unpkg.com/@aksell/ui/src/components/PillArrowBtn/standalone/PillArrowBtn.standalone.js';
```

## Step 5: Deliver

For `html` template:
```
cd <name>
open index.html
```

For `astro` template:
```
cd <name>
npm install
npm run dev
```

Tell the user where the project lives and how to open it.
