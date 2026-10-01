# Guardrails

Apply these to **every** style. The rules are summarised in SKILL.md; this file holds the CSS. Ledger rows cited here are in [contrast-ledger.md](contrast-ledger.md).

## Contents
- [Focus](#focus)
- [Motion](#motion)
- [Transparency and blur](#transparency-and-blur)
- [Forced colours (Windows High Contrast)](#forced-colours-windows-high-contrast)
- [Scoping](#scoping)
- [Fonts](#fonts)
- [Dark mode](#dark-mode)

## Focus
```css
:where([class*="theme-"]):focus-visible,
:where([class*="theme-"]) :focus-visible {
  outline: 3px solid var(--ui-focus);
  outline-offset: 3px;
}
/* Translucent surfaces: an offset ring sits over whatever is behind the component, which may be white.
   Use a two-tone ring (dark outline + white inner ring) so one of the two always reaches 3:1. */
.theme-glassmorphism:focus-visible,
.theme-glassmorphism :focus-visible {
  outline: 3px solid #0f172a;          /* 17.9:1 on white */
  outline-offset: 2px;
  box-shadow: 0 0 0 2px #ffffff, var(--ui-shadow);   /* white inner ring for dark backdrops */
}
```
Check focus contrast against the area **behind the outline**, not only the component's surface.
Never put `clip-path`, `mask` or `overflow: hidden` on a focusable element, because they clip its own outline. Draw clipped shapes on a pseudo-element instead (see the Cyberpunk recipe in the catalog).

## Motion
```css
@media (prefers-reduced-motion: reduce) {
  :where([class*="theme-"]) *, :where([class*="theme-"]) *::before, :where([class*="theme-"]) *::after {
    animation-duration: 0.01ms !important; animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important; scroll-behavior: auto !important;
  }
  :where([class*="theme-"]) [data-ui-motion] { transform: none !important; translate: none !important; rotate: none !important; }
}
```
Put `data-ui-motion` on elements whose transform is decorative or a hover effect, such as Neo-Brutalism's press offset, Scrapbook tilts or kinetic Maximalism type.

## Transparency and blur
```css
@supports not ((backdrop-filter: blur(1px)) or (-webkit-backdrop-filter: blur(1px))) {
  .ui-glass { background: var(--ui-bg); }   /* matches whether .ui-glass sits on the theme element or inside it */
}
@media (prefers-reduced-transparency: reduce) {
  .ui-glass { background: var(--ui-bg) !important; backdrop-filter: none !important; -webkit-backdrop-filter: none !important; }
}
```
The Glassmorphism surface `rgba(15, 23, 42, 0.75)` was chosen so white text stays at 7.95:1 even over a pure-white backdrop. Don't lower its alpha.

## Forced colours (Windows High Contrast)
Forced-colours mode replaces author backgrounds, so a control whose only visible shape is a background or a pseudo-element fill loses its boundary. Give such controls a real border in system colours:
```css
@media (forced-colors: active) {
  .cyber-btn, .cyber-card { border: 1px solid ButtonText; }
  .cyber-card { border-color: CanvasText; }
}
```
The generic `.ui-button` role pattern (SKILL.md, Workflow) already has a `2px solid transparent` border, and forced-colours mode paints that border visibly. Don't remove it.

## Scoping
A theme must not restyle the page that hosts it. Everything stays under `.theme-<id>` (or a class you own), and the guardrail selectors above already use `:where([class*="theme-"])`.
```css
/* Do not write: body { ... }  html { ... }  * { box-sizing: border-box }  button { ... }  h2 { ... } */
:where([class*="theme-"]), :where([class*="theme-"]) *, :where([class*="theme-"]) *::before, :where([class*="theme-"]) *::after { box-sizing: border-box; }
/* Standalone page you create: theme class on <html>, so this can never match a host page. */
.theme-swiss body { margin: 0; min-height: 100vh; background: var(--ui-bg); color: var(--ui-text); font-family: var(--ui-font-body); }
```
In a drop-in task (an existing app, a snippet, one component) the host keeps its `body`, margins and base font, so write no page-level rules at all. A bare selector inside a media query counts too, and so does one in the inline `<style>` of a demo or preview page you build around the component: write it as `.theme-<id> body` or put it on a wrapper class.

## Fonts
- All fonts named here are on Google Fonts under open licences, mostly the SIL OFL. Check the licence file you download.
- **Default: self-host.** Download the `woff2`, then declare it:
  ```css
  @font-face { font-family: "Press Start 2P"; src: url("/fonts/press-start-2p.woff2") format("woff2"); font-display: swap; }
  ```
- Use the Google Fonts `<link>` only if the project already loads remote fonts and its CSP allows `fonts.googleapis.com` and `fonts.gstatic.com`.
- Every stack ends in a generic family, so a blocked font degrades without breaking the page.
- Quote family names with exactly one pair of quotes: `"Press Start 2P"`, never `'"Press Start 2P"'`.
- Proprietary faces (Helvetica Neue, Didot, SF Pro) may be put *before* the open font as an optional local match. Never rely on them alone.

## Dark mode
The tokens are a single theme per style. To add dark mode, redefine the same roles under a selector (`.theme-bento-grid.dark { --ui-bg: …; }` or `@media (prefers-color-scheme: dark)`) and re-run the contrast check. Styles that are dark by nature (Cybercore, Synthwave, Pixel Art, Cyberpunk, Surrealism, Maximalism, Glassmorphism) and the parchment styles are light-only or dark-only by design. Say so instead of inverting them automatically.
