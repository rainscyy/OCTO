# OCTO Design System · Portable Kit

A self-contained design system extracted from the [OCTO workbench](https://github.com/rainscyy/OCTO) — for cross-project visual transfers.

## What's in this folder

| File | Purpose |
| --- | --- |
| `tokens.css` | All CSS variables (color, type, spacing, shadow). **Import first.** |
| `components.html` | Live component reference. Open in a browser. |
| `STYLE-GUIDE.md` | Design principles, dos & don'ts, migration checklist. |

## Quick start (3 steps)

```html
<!-- 1. Load the 4 fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=Fraunces:opsz,wght@9..144,400;9..144,500&family=IBM+Plex+Mono:wght@400;500&family=Noto+Serif+SC:wght@400;500&display=swap">

<!-- 2. Import tokens -->
<link rel="stylesheet" href="path/to/tokens.css">

<!-- 3. Build with var(--token-name) — never hard-code colors / type -->
```

```css
.my-button {
  background: var(--cobalt);
  color: #fff;
  border-radius: var(--r-md);
  padding: var(--sp-2) var(--sp-4);
  font-family: var(--sans);
  box-shadow: var(--shadow-cobalt);
}
```

## Transferring to another Claude session

Hand the other Claude one of these:

**Option A · Lightweight** — just the URL:

> Apply the design system from
> `https://github.com/rainscyy/OCTO/tree/main/design-system`
> to my existing app. Preserve all backend, routing, and state logic. Visual layer only.

**Option B · Heavy** — full instructions:

See [STYLE-GUIDE.md](./STYLE-GUIDE.md) for the migration checklist and behavioural constraints.

## Compatibility

- Plain HTML / CSS / JS — drop-in
- React / Vue / Svelte — wrap tokens in your component library
- Tailwind — extend `theme.colors` / `theme.fontFamily` from `tokens.css` values
- Native iOS / Android — use the token values manually (no auto-conversion yet)

## License

Code: MIT · Fonts: OFL 1.1 (all four, commercial use OK).

## Source

OCTO workbench prototype · 沙纯钰 (Raine) · 2026-04
