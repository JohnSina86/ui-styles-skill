# Tailwind mapping

Read this when the project uses Tailwind. Detect the version first (`package.json` -> `tailwindcss`), then use the matching section.

## Contents
- [Tailwind v4](#tailwind-v4)
- [Tailwind v3, or v4 with an explicit config](#tailwind-v3-or-v4-with-an-explicit-config)
- [No Tailwind](#no-tailwind)

## Tailwind v4
Use `@theme inline` so utilities follow scoped overrides. A plain `@theme` resolves `var()` once at `:root`, so a `.dark` override of `--ui-*` would not reach the utilities.

```css
@import "tailwindcss";
@theme inline {
  --color-ui-bg: var(--ui-bg);
  --color-ui-surface: var(--ui-surface);
  --color-ui-text: var(--ui-text);
  --color-ui-muted: var(--ui-text-muted);
  --color-ui-accent: var(--ui-accent);
  --color-ui-on-accent: var(--ui-on-accent);
  --color-ui-border: var(--ui-border);
  --color-ui-focus: var(--ui-focus);
  --radius-ui: var(--ui-radius);
  --shadow-ui: var(--ui-shadow);
  --font-ui-display: var(--ui-font-display);
  --font-ui-body: var(--ui-font-body);
}
```

This gives `bg-ui-surface`, `text-ui-text`, `border-ui-border`, `rounded-ui`, `shadow-ui`, `font-ui-display` and so on. Tailwind v4 does not auto-detect a JavaScript config, so don't add `theme.extend` unless the project already loads one with `@config`.

## Tailwind v3, or v4 with an explicit config
```js
// tailwind.config.js
module.exports = { theme: { extend: {
  colors: { ui: { bg: 'var(--ui-bg)', surface: 'var(--ui-surface)', text: 'var(--ui-text)', muted: 'var(--ui-text-muted)',
    accent: 'var(--ui-accent)', 'on-accent': 'var(--ui-on-accent)', border: 'var(--ui-border)', focus: 'var(--ui-focus)' } },
  borderRadius: { ui: 'var(--ui-radius)' }, boxShadow: { ui: 'var(--ui-shadow)' },
  fontFamily: { 'ui-display': 'var(--ui-font-display)', 'ui-body': 'var(--ui-font-body)' },
} } };
```

## No Tailwind
Use the custom properties directly, as in the recipes in [styles-catalog.md](styles-catalog.md).
