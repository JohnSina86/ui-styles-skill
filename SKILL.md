---
name: ui-styles
description: >-
  Design tokens, contrast-verified palettes and CSS/Tailwind recipes for 22
  distinctive UI styles (Neo-Brutalism, Glassmorphism, Bento Grid, Claymorphism,
  Cyberpunk, Swiss, Editorial and more). Use when the user names one of these
  styles or asks for a distinctive visual theme for new UI. Do not use to restyle
  a project that already has a design system unless the user asks for it.
---

# UI Styles & Visual Themes Skill (v1.1)

This skill turns an aesthetic request into production CSS: one token block per style with fixed role names, verified contrast, and shared accessibility guardrails. Detailed component recipes (button, card, input) for six styles are in [`references/styles-catalog.md`](references/styles-catalog.md). For the other sixteen, build components from the tokens using the pattern in §6.

---

## 0. Before you style (mandatory)

1. **Existing design system first.** If the project already has tokens, a theme file or a component library, do not replace it. Map the chosen style onto the existing tokens as an accent layer, and only replace the system if the user asks.
2. **Detect the Tailwind version** (`package.json` → `tailwindcss`) and pick the mapping in §2.
3. **Font policy.** Check the project's CSP and asset policy before adding fonts. Prefer self-hosting (§5.5). Never inject a remote font link by default.
4. **Pick a style.** Match the request to a style below. If no style was named, propose two styles, each with one line of reasoning drawn from its *Best for* and *Avoid when* lines.

## 1. The 5 archetypes

| Archetype | Styles |
| :--- | :--- |
| Dimensional & Tactile | Claymorphism, Neumorphism, Glassmorphism |
| Graphic & Modernist | Neo-Brutalism, Swiss, Minimalism, Maximalism, Editorial, Bento Grid |
| Retro & Nostalgic | Y2K, Pixel Art, Synthwave, Victorian |
| High-Tech & Futuristic | Cybercore, Cyberpunk |
| Artistic & Organic | Scrapbook, Surrealism, Conceptual Sketch, Ethereal, Bohemian, Luxury Typography, Wabi-Sabi |

## 2. Token contract

Every style defines the same roles, so components never hard-code colours:

| Token | Role |
| :--- | :--- |
| `--ui-bg` | Page background |
| `--ui-surface` | Cards, panels, inputs |
| `--ui-text` | Body text (≥ 4.5:1 on bg and surface) |
| `--ui-text-muted` | Secondary text (≥ 4.5:1 on bg and surface) |
| `--ui-accent` / `--ui-on-accent` | Primary action fill and its label (≥ 4.5:1) |
| `--ui-border` | Boundaries of controls such as inputs, toggles and outline buttons (≥ 3:1, WCAG 1.4.11) |
| `--ui-focus` | Focus indicator (≥ 3:1 on bg and surface) |
| `--ui-radius`, `--ui-shadow` | Shape and elevation |
| `--ui-font-display`, `--ui-font-body` | Font stacks with generic fallbacks |
| *Optional:* `--ui-border-width`, `--ui-blur`, `--ui-backdrop`, `--ui-tilt`, `--ui-chrome`, `--ui-pattern`, `--ui-tracking`, `--ui-leading` | Style-specific values that components consume |

A token block contains **only custom properties**, so adding the class to `<html>` never changes layout by itself. Components consume the tokens.

Apply a style by adding its class (`.theme-neo-brutalism`) to `<html>` or to any container. The blocks are class-scoped, so different sections can use different styles.

### Tailwind mapping
- **Tailwind v4.** Use `@theme inline` so utilities follow scoped overrides. A plain `@theme` resolves `var()` once at `:root`.
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
  This gives utilities such as `bg-ui-surface`, `text-ui-text`, `border-ui-border`, `rounded-ui`, `shadow-ui` and `font-ui-display`. Tailwind v4 does not auto-detect a JS config, so don't add `theme.extend` unless the project already loads one with `@config`.
- **Tailwind v3, or v4 with an explicit `@config`:**
  ```js
  // tailwind.config.js
  module.exports = { theme: { extend: {
    colors: { ui: { bg: 'var(--ui-bg)', surface: 'var(--ui-surface)', text: 'var(--ui-text)', muted: 'var(--ui-text-muted)',
      accent: 'var(--ui-accent)', 'on-accent': 'var(--ui-on-accent)', border: 'var(--ui-border)', focus: 'var(--ui-focus)' } },
    borderRadius: { ui: 'var(--ui-radius)' }, boxShadow: { ui: 'var(--ui-shadow)' },
    fontFamily: { 'ui-display': 'var(--ui-font-display)', 'ui-body': 'var(--ui-font-body)' },
  } } };
  ```
- **No Tailwind:** use the custom properties directly.

## 3. Contrast contract

Every role pair in §4 was computed with the WCAG 2.x relative-luminance formula, and all pass: text and muted text ≥ 4.5:1 on bg and surface, on-accent ≥ 4.5:1 on accent, border and focus ≥ 3:1 on bg and surface. Colours listed under **Decorative only** fail at least one of these. Use them for ornament, rules or large text (≥ 24px, or ≥ 18.66px bold) only, as their notes say.

If you change a token, recompute the ratio. Don't judge contrast by eye. Translucent surfaces are checked as composited over the **lightest** backdrop they can sit on.

---

## 4. Style directory (22 styles)

### 1. Claymorphism
* **Archetype**: Dimensional & Tactile
* **Visual DNA**: Puffy, inflated clay shapes: pastel surfaces with outer shadows tinted from the surface colour plus soft inner highlights. Friendly and tactile.
* **Tokens** (every role pair verified — see §3):
```css
.theme-claymorphism {
  --ui-bg: #fdf2f8;
  --ui-surface: #ffd6e7;
  --ui-text: #3b1d2e;
  --ui-text-muted: #6b3a55;
  --ui-accent: #7c3aed;
  --ui-on-accent: #ffffff;
  --ui-border: #a3487a;
  --ui-focus: #5b21b6;
  --ui-radius: 24px;
  --ui-shadow: 12px 12px 24px rgba(163, 72, 122, 0.25), -12px -12px 24px rgba(255, 255, 255, 0.9), inset -6px -6px 12px rgba(59, 29, 46, 0.08), inset 6px 6px 12px rgba(255, 255, 255, 0.7);
  --ui-font-display: "Nunito", ui-sans-serif, system-ui, sans-serif;
  --ui-font-body: "Nunito", ui-sans-serif, system-ui, sans-serif;
}
```
* **Decorative only (not for text or control boundaries)**: #c7f2e3 mint; #e9d5ff lavender
* **Best for**: Gamified apps, education, child-friendly products, onboarding steps.
* **Avoid when**: Data-dense dashboards and financial terminals: the heavy shadows cost space and weaken grouping cues (ux-laws #4 Proximity, #14 Uniform Connectedness).

---

### 2. Cybercore
* **Archetype**: High-Tech & Futuristic
* **Visual DNA**: Technical wireframes, HUD overlays, coordinates, monospaced read-outs, thin geometric lines.
* **Tokens** (every role pair verified — see §3):
```css
.theme-cybercore {
  --ui-bg: #0a0b0e;
  --ui-surface: #0d0f14;
  --ui-text: #e6fbff;
  --ui-text-muted: #8fb3bd;
  --ui-accent: #00f0ff;
  --ui-on-accent: #001a1d;
  --ui-border: #00a9b5;
  --ui-focus: #00f0ff;
  --ui-radius: 2px;
  --ui-shadow: inset 0 0 15px rgba(0, 240, 255, 0.06);
  --ui-font-display: "JetBrains Mono", ui-monospace, monospace;
  --ui-font-body: "JetBrains Mono", ui-monospace, monospace;
}
```
* **Decorative only (not for text or control boundaries)**: #506040 tactical olive (2.9:1 — lines only)
* **Best for**: Dev tools, terminal interfaces, gaming overlays, telemetry.
* **Avoid when**: Casual e-commerce and lifestyle content: all-monospace body text slows reading, and HUD styling fights familiar shopping conventions (ux-laws #3 Jakob).

---

### 3. Neo-Brutalism
* **Archetype**: Graphic & Modernist
* **Visual DNA**: Raw high contrast: thick black borders, hard offset shadows with zero blur, saturated colour blocks.
* **Tokens** (every role pair verified — see §3):
```css
.theme-neo-brutalism {
  --ui-bg: #fffdf5;
  --ui-surface: #ffffff;
  --ui-text: #000000;
  --ui-text-muted: #3f3f46;
  --ui-accent: #ffde59;
  --ui-on-accent: #000000;
  --ui-border: #000000;
  --ui-focus: #1d4ed8;
  --ui-radius: 8px;
  --ui-shadow: 5px 5px 0 #000000;
  --ui-font-display: "Space Grotesk", ui-sans-serif, system-ui, sans-serif;
  --ui-font-body: "Space Grotesk", ui-sans-serif, system-ui, sans-serif;
  --ui-border-width: 3px;
  /* hover: transform: translate(2px, 2px); box-shadow: 3px 3px 0 #000000; */
}
```
* **Decorative only (not for text or control boundaries)**: #ff6b6b coral (black text only); #4deeea cyan (black text only)
* **Best for**: SaaS marketing, design portfolios, Gen-Z fintech, productivity apps.
* **Avoid when**: Conservative enterprise and healthcare, where the loud styling undermines trust (ux-laws #17 Aesthetic-Usability).

---

### 4. Scrapbook
* **Archetype**: Artistic & Organic
* **Visual DNA**: Tactile collage: paper cut-outs, tape, stamps, hand-drawn notes, Polaroid frames, slightly rotated decorative elements.
* **Tokens** (every role pair verified — see §3):
```css
.theme-scrapbook {
  --ui-bg: #f4ece1;
  --ui-surface: #fffdf9;
  --ui-text: #2b2622;
  --ui-text-muted: #5c5249;
  --ui-accent: #b4232c;
  --ui-on-accent: #ffffff;
  --ui-border: #857561;
  --ui-focus: #1d4ed8;
  --ui-radius: 3px;
  --ui-shadow: 2px 4px 12px rgba(0, 0, 0, 0.08);
  --ui-font-display: "Caveat", cursive;
  --ui-font-body: "Lora", ui-serif, Georgia, serif;
  --ui-tilt: -1.5deg; /* apply rotate(var(--ui-tilt)) to decorative wrappers only — never to inputs or body text */
}
```
* **Decorative only (not for text or control boundaries)**: #e2dac9 paper edge (1.4:1 — decorative); washi pastels
* **Best for**: Creative portfolios, moodboards, storytelling blogs, invitations.
* **Avoid when**: High-efficiency workflows and multi-step funnels: rotated, overlapping items break alignment cues (ux-laws #12 Prägnanz).

---

### 5. Surrealism
* **Archetype**: Artistic & Organic
* **Visual DNA**: Dreamlike depth, floating objects, unexpected scale, atmospheric radial light.
* **Tokens** (every role pair verified — see §3):
```css
.theme-surrealism {
  --ui-bg: #0d0814;
  --ui-surface: #2e1a47;
  --ui-text: #f5ecff;
  --ui-text-muted: #c9b6e4;
  --ui-accent: #ffb347;
  --ui-on-accent: #1a0f00;
  --ui-border: #9b7cc4;
  --ui-focus: #ffb347;
  --ui-radius: 24px;
  --ui-shadow: 0 20px 30px rgba(110, 40, 200, 0.3);
  --ui-font-display: "Syne", ui-sans-serif, system-ui, sans-serif;
  --ui-font-body: "Inter", ui-sans-serif, system-ui, sans-serif;
  --ui-backdrop: radial-gradient(circle at 50% 20%, #2e1a47, #0d0814);
}
```
* **Decorative only (not for text or control boundaries)**: #6e28c8 violet glow
* **Best for**: High-concept fashion, music releases, interactive art showcases.
* **Avoid when**: Utility apps and forms: disorientation is the point of the style and the opposite of a usable form (ux-laws #3 Jakob, #12 Prägnanz).

---

### 6. Y2K Aesthetic
* **Archetype**: Retro & Nostalgic
* **Visual DNA**: Early-2000s cyber-optimism: glossy candy buttons, chrome sheen, starbursts, bubble type, iridescence.
* **Tokens** (every role pair verified — see §3):
```css
.theme-y2k {
  --ui-bg: #f0f9ff;
  --ui-surface: #ffffff;
  --ui-text: #1e1b4b;
  --ui-text-muted: #4c4a7a;
  --ui-accent: #c2006a;
  --ui-on-accent: #ffffff;
  --ui-border: #6b7fa8;
  --ui-focus: #0369a1;
  --ui-radius: 9999px;
  --ui-shadow: 0 4px 10px rgba(0, 180, 255, 0.3), inset 0 2px 4px rgba(255, 255, 255, 0.8);
  --ui-font-display: "Outfit", ui-sans-serif, system-ui, sans-serif;
  --ui-font-body: "Outfit", ui-sans-serif, system-ui, sans-serif;
  --ui-chrome: linear-gradient(180deg, #ffffff 0%, #e2e8f0 50%, #cbd5e1 100%); /* decorative fills; keep text on --ui-surface */
}
```
* **Decorative only (not for text or control boundaries)**: #ff72b6 bubblegum (decor/large); #98eecc lime (decor); chrome gradient
* **Best for**: Music platforms, streetwear, retro games, youth entertainment.
* **Avoid when**: B2B, legal and financial platforms.

---

### 7. Pixel Art
* **Archetype**: Retro & Nostalgic
* **Visual DNA**: 8/16-bit arcade: visible raster grid, stepped block borders, bitmap fonts, restricted palette (PICO-8 here).
* **Tokens** (every role pair verified — see §3):
```css
.theme-pixel-art {
  --ui-bg: #1d2b53;
  --ui-surface: #000000;
  --ui-text: #fff1e8;
  --ui-text-muted: #c2c3c7;
  --ui-accent: #ffec27;
  --ui-on-accent: #000000;
  --ui-border: #fff1e8;
  --ui-focus: #ff77a8;
  --ui-radius: 0;
  --ui-shadow: 4px 0 0 var(--ui-border), -4px 0 0 var(--ui-border), 0 4px 0 var(--ui-border), 0 -4px 0 var(--ui-border);
  --ui-font-display: "Press Start 2P", ui-monospace, monospace;
  --ui-font-body: "VT323", ui-monospace, monospace;
  /* sprites: img, canvas { image-rendering: pixelated; } */
}
```
* **Decorative only (not for text or control boundaries)**: #ff004d red; #00e436 green; #29adff blue (PICO-8)
* **Best for**: Retro gaming sites, indie dev hubs, easter eggs, community pages.
* **Avoid when**: Long-form reading: use Press Start 2P only for headings and labels (it is hard to read in paragraphs).

---

### 8. Synthwave
* **Archetype**: Retro & Nostalgic
* **Visual DNA**: 1980s retrowave: neon magenta and cyan glows, perspective grids, neon sunsets, scanlines.
* **Tokens** (every role pair verified — see §3):
```css
.theme-synthwave {
  --ui-bg: #120422;
  --ui-surface: #1a0826;
  --ui-text: #fdf4ff;
  --ui-text-muted: #d8b4fe;
  --ui-accent: #ff007f;
  --ui-on-accent: #120422;
  --ui-border: #ff007f;
  --ui-focus: #00f0ff;
  --ui-radius: 6px;
  --ui-shadow: 0 0 15px rgba(255, 0, 127, 0.4), inset 0 0 15px rgba(0, 240, 255, 0.2);
  --ui-font-display: "Orbitron", ui-sans-serif, system-ui, sans-serif;
  --ui-font-body: "Inter", ui-sans-serif, system-ui, sans-serif;
  /* text-shadow: 0 0 8px var(--ui-accent) — headings ≥24px only; glow blurs small text */
}
```
* **Decorative only (not for text or control boundaries)**: #ffe600 solar gold; #00f0ff cyan glow
* **Best for**: Audio tools, streaming channels, gaming hardware, night-event pages.
* **Avoid when**: Daytime reading and public-service sites.

---

### 9. Glassmorphism
* **Archetype**: Dimensional & Tactile
* **Visual DNA**: Frosted translucent panels with backdrop blur over a dark or saturated backdrop, hairline specular edges.
* **Tokens** (every role pair verified — see §3):
```css
.theme-glassmorphism {
  --ui-bg: #0f172a;
  --ui-surface: rgba(15, 23, 42, 0.75);
  --ui-text: #ffffff;
  --ui-text-muted: #cbd5e1;
  --ui-accent: #38bdf8;
  --ui-on-accent: #0f172a;
  --ui-border: #94a3b8;
  --ui-focus: #7dd3fc;
  --ui-radius: 20px;
  --ui-shadow: 0 8px 32px rgba(15, 23, 42, 0.25);
  --ui-font-display: "Inter", ui-sans-serif, system-ui, sans-serif;
  --ui-font-body: "Inter", ui-sans-serif, system-ui, sans-serif;
  --ui-blur: 16px; /* on .ui-glass panels: backdrop-filter: blur(var(--ui-blur)) */
}
```
* **Decorative only (not for text or control boundaries)**: rgba(255,255,255,.25) hairline (decorative); gradient orbs
* **Best for**: Floating control bars, OS-style panels, premium tech landing pages.
* **Avoid when**: Text-heavy surfaces over busy or light imagery. Use only over a dark or saturated backdrop — the tint is set so text still passes over pure white.

---

### 10. Neumorphism (Soft UI)
* **Archetype**: Dimensional & Tactile
* **Visual DNA**: Extruded-plastic surfaces that look sculpted from the background; monochrome.
* **Tokens** (every role pair verified — see §3):
```css
.theme-neumorphism {
  --ui-bg: #e0e5ec;
  --ui-surface: #e0e5ec;
  --ui-text: #1f2937;
  --ui-text-muted: #4b5563;
  --ui-accent: #3b5bdb;
  --ui-on-accent: #ffffff;
  --ui-border: #737b8c;
  --ui-focus: #1d4ed8;
  --ui-radius: 16px;
  --ui-shadow: 9px 9px 16px rgba(163, 177, 198, 0.6), -9px -9px 16px rgba(255, 255, 255, 0.8);
  --ui-font-display: "Inter", ui-sans-serif, system-ui, sans-serif;
  --ui-font-body: "Inter", ui-sans-serif, system-ui, sans-serif;
  /* pressed: box-shadow: inset 6px 6px 10px #a3b1c6, inset -6px -6px 10px #ffffff; */
  /* inputs and toggles MUST also get border: 1px solid var(--ui-border) — the shadows alone are ~1.3:1 */
}
```
* **Decorative only (not for text or control boundaries)**: #a3b1c6 dark shadow; #ffffff light shadow
* **Best for**: Smart-home controls, hardware simulators, synth dials.
* **Avoid when**: Forms and anything where state must be obvious: pressed vs raised is a low-contrast difference (ux-laws #13 Similarity).

---

### 11. Bento Grid
* **Archetype**: Graphic & Modernist
* **Visual DNA**: Asymmetric modular grid of rounded cards, compact widgets, mixed spans.
* **Tokens** (every role pair verified — see §3):
```css
.theme-bento-grid {
  --ui-bg: #fafafa;
  --ui-surface: #ffffff;
  --ui-text: #18181b;
  --ui-text-muted: #52525b;
  --ui-accent: #4f46e5;
  --ui-on-accent: #ffffff;
  --ui-border: #71717a;
  --ui-focus: #4f46e5;
  --ui-radius: 20px;
  --ui-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
  --ui-font-display: "Plus Jakarta Sans", ui-sans-serif, system-ui, sans-serif;
  --ui-font-body: "Inter", ui-sans-serif, system-ui, sans-serif;
  /* container: display: grid; grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr)); gap: 16px; */
}
```
* **Decorative only (not for text or control boundaries)**: #e4e4e7 card edge (1.3:1 — decorative, never on inputs)
* **Best for**: Feature highlights, SaaS homepages, portfolio and executive summaries.
* **Avoid when**: Sequential content, where spans and explicit placement make the visual order differ from DOM order (WCAG 1.3.2, 2.4.3 focus order). Keep source order equal to visual order.

---

### 12. Editorial Design
* **Archetype**: Graphic & Modernist
* **Visual DNA**: Magazine layout: dramatic serif headlines, multi-column text, pull quotes, drop caps, rules instead of shadows.
* **Tokens** (every role pair verified — see §3):
```css
.theme-editorial {
  --ui-bg: #f9f9f8;
  --ui-surface: #ffffff;
  --ui-text: #1c1c1a;
  --ui-text-muted: #57534e;
  --ui-accent: #9a3412;
  --ui-on-accent: #ffffff;
  --ui-border: #1c1c1a;
  --ui-focus: #9a3412;
  --ui-radius: 0;
  --ui-shadow: none;
  --ui-font-display: "Playfair Display", ui-serif, Georgia, serif;
  --ui-font-body: "Newsreader", ui-serif, Georgia, serif;
  /* @media (min-width: 64rem) { .ui-columns { column-count: 2; column-gap: 32px; } } — single column below */
}
```
* **Decorative only (not for text or control boundaries)**: none
* **Best for**: Journalism, essays, literature platforms, fashion storytelling.
* **Avoid when**: Toolbars and data entry.

---

### 13. Swiss Design (International Typographic Style)
* **Archetype**: Graphic & Modernist
* **Visual DNA**: Strict mathematical grid, asymmetric balance, grotesque sans, single bold accent, no decoration.
* **Tokens** (every role pair verified — see §3):
```css
.theme-swiss {
  --ui-bg: #ffffff;
  --ui-surface: #ffffff;
  --ui-text: #000000;
  --ui-text-muted: #404040;
  --ui-accent: #d00000;
  --ui-on-accent: #ffffff;
  --ui-border: #000000;
  --ui-focus: #002fa7;
  --ui-radius: 0;
  --ui-shadow: none;
  --ui-font-display: "Inter", ui-sans-serif, system-ui, sans-serif;
  --ui-font-body: "Inter", ui-sans-serif, system-ui, sans-serif;
  /* headings only: text-transform: uppercase; letter-spacing: -0.03em; body stays sentence case */
}
```
* **Decorative only (not for text or control boundaries)**: #ff0000 Swiss red (4.0:1 — rules, blocks, text ≥24px only)
* **Best for**: Architecture, design agencies, transit information, minimalist publications.
* **Avoid when**: Nothing structurally, but uppercase body text and pure #ff0000 small text are not acceptable — see the colour notes.

---

### 14. Minimalism
* **Archetype**: Graphic & Modernist
* **Visual DNA**: Intentional whitespace, removal of non-essential elements, content first.
* **Tokens** (every role pair verified — see §3):
```css
.theme-minimalism {
  --ui-bg: #ffffff;
  --ui-surface: #ffffff;
  --ui-text: #18181b;
  --ui-text-muted: #71717a;
  --ui-accent: #18181b;
  --ui-on-accent: #ffffff;
  --ui-border: #8a8a93;
  --ui-focus: #18181b;
  --ui-radius: 6px;
  --ui-shadow: none;
  --ui-font-display: "Inter", ui-sans-serif, system-ui, sans-serif;
  --ui-font-body: "Inter", ui-sans-serif, system-ui, sans-serif;
}
```
* **Decorative only (not for text or control boundaries)**: #f4f4f5 hairline (1.1:1 — decorative, never on inputs)
* **Best for**: Writing tools, modern e-commerce, developer portfolios, luxury brands.
* **Avoid when**: Hiding affordances: icon-only buttons and hairline inputs are the usual minimalism failures (ux-laws #3 Jakob).

---

### 15. Maximalism
* **Archetype**: Graphic & Modernist
* **Visual DNA**: Expressive abundance: dense layering, clashing patterns, saturated colour, kinetic type.
* **Tokens** (every role pair verified — see §3):
```css
.theme-maximalism {
  --ui-bg: #1a0033;
  --ui-surface: #2b0057;
  --ui-text: #ffffff;
  --ui-text-muted: #f0d9ff;
  --ui-accent: #ffe600;
  --ui-on-accent: #000000;
  --ui-border: #ffe600;
  --ui-focus: #00ffd1;
  --ui-radius: 0;
  --ui-shadow: 6px 6px 0 #ff0055;
  --ui-font-display: "Anton", ui-sans-serif, system-ui, sans-serif;
  --ui-font-body: "Inter", ui-sans-serif, system-ui, sans-serif;
  --ui-pattern: repeating-linear-gradient(45deg, #ff0055 0 20px, #7a00ff 20px 40px); /* behind solid --ui-surface text panels only */
}
```
* **Decorative only (not for text or control boundaries)**: #ff0055 magenta; #7a00ff violet; pattern fills (behind solid panels only)
* **Best for**: Festivals, pop-culture magazines, music events, campaign drops.
* **Avoid when**: Form-heavy transactions (ux-laws #1 Hick, #12 Prägnanz).

---

### 16. Luxury Typography
* **Archetype**: Artistic & Organic
* **Visual DNA**: High-contrast Didone serifs, hairline stems, wide tracking on short labels, monochrome restraint with gold ornament.
* **Tokens** (every role pair verified — see §3):
```css
.theme-luxury {
  --ui-bg: #f7f4ee;
  --ui-surface: #ffffff;
  --ui-text: #0b0b0c;
  --ui-text-muted: #4a4540;
  --ui-accent: #0b0b0c;
  --ui-on-accent: #f7f4ee;
  --ui-border: #7a6440;
  --ui-focus: #0b0b0c;
  --ui-radius: 0;
  --ui-shadow: none;
  --ui-font-display: "Bodoni Moda", ui-serif, Georgia, serif;
  --ui-font-body: "Cormorant Garamond", ui-serif, Georgia, serif;
  /* labels only: text-transform: uppercase; letter-spacing: 0.25em; */
}
```
* **Decorative only (not for text or control boundaries)**: #c5a880 brushed gold (2.1:1 — ornament only)
* **Best for**: Fine jewellery, luxury real estate, fragrance, fine dining.
* **Avoid when**: Fast technical dashboards.

---

### 17. Conceptual Sketch
* **Archetype**: Artistic & Organic
* **Visual DNA**: Hand-drawn wireframes, pencil outlines, graph-paper backdrop, wobbly borders, annotation arrows.
* **Tokens** (every role pair verified — see §3):
```css
.theme-sketch {
  --ui-bg: #fcfbf7;
  --ui-surface: #ffffff;
  --ui-text: #2c2c2c;
  --ui-text-muted: #555555;
  --ui-accent: #1d4ed8;
  --ui-on-accent: #ffffff;
  --ui-border: #2c2c2c;
  --ui-focus: #c2410c;
  --ui-radius: 255px 15px 225px 15px / 15px 225px 15px 255px;
  --ui-shadow: none;
  --ui-font-display: "Architects Daughter", cursive;
  --ui-font-body: "Inter", ui-sans-serif, system-ui, sans-serif;
  --ui-border-width: 2px;
  --ui-backdrop: radial-gradient(#d1d5db 1px, transparent 1px) 0 0 / 16px 16px;
}
```
* **Decorative only (not for text or control boundaries)**: #d1d5db grid dots; #0f2b5c blueprint navy (alt. bg with #ffffff text)
* **Best for**: Prototyping tools, concept docs, planning, education.
* **Avoid when**: Polished checkout flows: the "unfinished" look lowers trust at payment (ux-laws #17).

---

### 18. Ethereal
* **Archetype**: Artistic & Organic
* **Visual DNA**: Luminous ambient glow, soft pastel gradients, gentle diffusion, calm and light typography.
* **Tokens** (every role pair verified — see §3):
```css
.theme-ethereal {
  --ui-bg: #f6f4fb;
  --ui-surface: #fbfaff;
  --ui-text: #2e2a47;
  --ui-text-muted: #5b5675;
  --ui-accent: #6d28d9;
  --ui-on-accent: #ffffff;
  --ui-border: #8b84a8;
  --ui-focus: #6d28d9;
  --ui-radius: 24px;
  --ui-shadow: 0 20px 40px rgba(180, 160, 220, 0.15);
  --ui-font-display: "Cormorant Garamond", ui-serif, Georgia, serif;
  --ui-font-body: "Urbanist", ui-sans-serif, system-ui, sans-serif;
  --ui-backdrop: linear-gradient(135deg, #e8e5f3, #fcefef 50%, #e0f4f4);
  /* body font-weight ≥ 400: "thin" type fails legibility */
}
```
* **Decorative only (not for text or control boundaries)**: #e8e5f3 mist; #fcefef blush; #e0f4f4 opal
* **Best for**: Meditation, wellness, organic skincare, journals.
* **Avoid when**: Urgent financial or operational consoles.

---

### 19. Bohemian (Boho)
* **Archetype**: Artistic & Organic
* **Visual DNA**: Earthy terracotta and sage, botanical illustration, hand-crafted textures, sun-washed warmth.
* **Tokens** (every role pair verified — see §3):
```css
.theme-bohemian {
  --ui-bg: #f5efeb;
  --ui-surface: #fbf8f5;
  --ui-text: #4a3e35;
  --ui-text-muted: #6b5a4c;
  --ui-accent: #9c4a32;
  --ui-on-accent: #ffffff;
  --ui-border: #8a7360;
  --ui-focus: #9c4a32;
  --ui-radius: 12px;
  --ui-shadow: 0 4px 14px rgba(74, 62, 53, 0.08);
  --ui-font-display: "Fraunces", ui-serif, Georgia, serif;
  --ui-font-body: "Lora", ui-serif, Georgia, serif;
}
```
* **Decorative only (not for text or control boundaries)**: #c86d51 terracotta (3.2:1 — large text/decor); #d8a243 mustard (2.0:1 — decor); #8a9a86 sage (decor)
* **Best for**: Artisan markets, eco goods, travel logs, coffee shops.
* **Avoid when**: Cyber tools and infrastructure consoles.

---

### 20. Victorian
* **Archetype**: Retro & Nostalgic
* **Visual DNA**: 19th-century ornament: engraved filigree, double rules, jewel tones on parchment, decorative capitals.
* **Tokens** (every role pair verified — see §3):
```css
.theme-victorian {
  --ui-bg: #ebdcb9;
  --ui-surface: #f3e9d2;
  --ui-text: #4a0e17;
  --ui-text-muted: #5c3a2e;
  --ui-accent: #4a0e17;
  --ui-on-accent: #f3e9d2;
  --ui-border: #4a0e17;
  --ui-focus: #0b2b1e;
  --ui-radius: 2px;
  --ui-shadow: inset 0 0 20px rgba(74, 14, 23, 0.2);
  --ui-font-display: "Cinzel Decorative", ui-serif, Georgia, serif;
  --ui-font-body: "Lora", ui-serif, Georgia, serif;
  --ui-border-width: 4px; /* cards: border: var(--ui-border-width) double var(--ui-border) */
  /* Cinzel Decorative for display only — unreadable as body text */
}
```
* **Decorative only (not for text or control boundaries)**: #b38f4d tarnished brass (ornament); #0b2b1e emerald
* **Best for**: Heritage distilleries, escape rooms, archives, dark-academia themes.
* **Avoid when**: Mobile utilities: heavy ornament costs space on small screens.

---

### 21. Cyberpunk
* **Archetype**: High-Tech & Futuristic
* **Visual DNA**: Dystopian high-tech: angular cut corners, scanlines, high-voltage yellow and cyan on carbon.
* **Tokens** (every role pair verified — see §3):
```css
.theme-cyberpunk {
  --ui-bg: #0c0c0e;
  --ui-surface: #0d0d11;
  --ui-text: #fcee09;
  --ui-text-muted: #c9c9d1;
  --ui-accent: #fcee09;
  --ui-on-accent: #000000;
  --ui-border: #fcee09;
  --ui-focus: #00f0ff;
  --ui-radius: 0;
  --ui-shadow: none;
  --ui-font-display: "Rajdhani", ui-sans-serif, system-ui, sans-serif;
  --ui-font-body: "Chakra Petch", ui-sans-serif, system-ui, sans-serif;
  /* cut corners: see the catalog recipe — never clip-path the focusable element itself */
}
```
* **Decorative only (not for text or control boundaries)**: #00f0ff cyan (hover fill, black text); #ff0055 magenta (decor)
* **Best for**: Esports, sci-fi gaming, streaming, hardware launches.
* **Avoid when**: Long reading: yellow body text on black is tiring in quantity — keep it for short UI text.

---

### 22. Wabi-Sabi
* **Archetype**: Artistic & Organic
* **Visual DNA**: Japanese aesthetic of impermanence: asymmetric balance, raw textures (stone, clay, linen), quiet space.
* **Tokens** (every role pair verified — see §3):
```css
.theme-wabi-sabi {
  --ui-bg: #edeae1;
  --ui-surface: #f4f2ec;
  --ui-text: #232323;
  --ui-text-muted: #57534e;
  --ui-accent: #5e4636;
  --ui-on-accent: #ffffff;
  --ui-border: #857565;
  --ui-focus: #232323;
  --ui-radius: 4px;
  --ui-shadow: 0 2px 10px rgba(35, 35, 35, 0.06);
  --ui-font-display: "Shippori Mincho", ui-serif, Georgia, serif;
  --ui-font-body: "Cormorant Garamond", ui-serif, Georgia, serif;
  --ui-tracking: 0.04em;
  --ui-leading: 1.8;
}
```
* **Decorative only (not for text or control boundaries)**: #9b8373 raw clay (3.0:1 — decor); #6e6b65 slate
* **Best for**: Architecture studios, tea houses, ceramics, mindful publications.
* **Avoid when**: Dense data views.


---

## 5. Guardrails (apply to every style)

### 5.1 Focus
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

### 5.2 Motion
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

### 5.3 Transparency and blur
```css
@supports not ((backdrop-filter: blur(1px)) or (-webkit-backdrop-filter: blur(1px))) {
  .ui-glass { background: var(--ui-bg); }   /* matches whether .ui-glass sits on the theme element or inside it */
}
@media (prefers-reduced-transparency: reduce) {
  .ui-glass { background: var(--ui-bg) !important; backdrop-filter: none !important; -webkit-backdrop-filter: none !important; }
}
```
The Glassmorphism surface `rgba(15, 23, 42, 0.75)` was chosen so white text stays at 7.95:1 even over a pure-white backdrop. Don't lower its alpha.

### 5.4 Forced colours (Windows High Contrast)
Forced-colours mode replaces author backgrounds, so a control whose only visible shape is a background or a pseudo-element fill loses its boundary. Give such controls a real border in system colours:
```css
@media (forced-colors: active) {
  .cyber-btn, .cyber-card { border: 1px solid ButtonText; }
  .cyber-card { border-color: CanvasText; }
}
```
The generic `.ui-button` in §6 already has a `2px solid transparent` border, and forced-colours mode paints that border visibly. Don't remove it.

### 5.5 Fonts
- All fonts named here are on Google Fonts under open licences, mostly the SIL OFL. Check the licence file you download.
- **Default: self-host.** Download the `woff2`, then declare it:
  ```css
  @font-face { font-family: "Press Start 2P"; src: url("/fonts/press-start-2p.woff2") format("woff2"); font-display: swap; }
  ```
- Use the Google Fonts `<link>` only if the project already loads remote fonts and its CSP allows `fonts.googleapis.com` and `fonts.gstatic.com`.
- Every stack ends in a generic family, so a blocked font degrades without breaking the page.
- Quote family names with exactly one pair of quotes: `"Press Start 2P"`, never `'"Press Start 2P"'`.
- Proprietary faces (Helvetica Neue, Didot, SF Pro) may be put *before* the open font as an optional local match. Never rely on them alone.

### 5.6 Dark mode
The tokens are a single theme per style. To add dark mode, redefine the same roles under a selector (`.theme-bento-grid.dark { --ui-bg: …; }` or `@media (prefers-color-scheme: dark)`) and re-run the contrast check. Styles that are dark by nature (Cybercore, Synthwave, Pixel Art, Cyberpunk, Surrealism, Maximalism, Glassmorphism) and the parchment styles are light-only or dark-only by design. Say so instead of inverting them automatically.

---

## 6. Workflow

1. Do §0.
2. **Apply tokens.** Paste the style's token block into the global stylesheet. Add the Tailwind mapping from §2 if the project uses Tailwind. Add the guardrails from §5 once.
3. **Build components from roles.** For the six styles in the catalog, use those recipes. For the rest, use this pattern:
   ```css
   .ui-card   { background: var(--ui-surface); color: var(--ui-text); border-radius: var(--ui-radius); box-shadow: var(--ui-shadow); padding: 24px; }
   .ui-button { background: var(--ui-accent); color: var(--ui-on-accent); border: 2px solid transparent; border-radius: var(--ui-radius);
                font-family: var(--ui-font-display); min-height: 44px; padding: 10px 20px; cursor: pointer; }
   .ui-input  { background: var(--ui-surface); color: var(--ui-text); border: 1px solid var(--ui-border); border-radius: var(--ui-radius);
                min-height: 44px; padding: 8px 12px; font-family: var(--ui-font-body); }
   ```
4. **Verify:**
   - Contrast: recompute any changed pair (§3).
   - Focus is visible on every interactive element (§5.1).
   - Reduced motion and reduced transparency are honoured.
   - Target size: at least 24×24 CSS px, or the WCAG 2.2 AA 2.5.8 spacing exception. Aim for 44×44 on touch-first surfaces.
   - For a UX review of the result, use the `ux-laws` skill. That skill grades structure, not the chosen aesthetic.
