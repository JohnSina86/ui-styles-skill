# Tokens: Artistic & Organic

Read this file **after** choosing a style from the SKILL.md style index. Every block contains only custom properties (see the token contract in SKILL.md). Colours were verified against WCAG 2.x: see [contrast-ledger.md](contrast-ledger.md).

## Contents
- [Scrapbook](#scrapbook)
- [Surrealism](#surrealism)
- [Luxury Typography](#luxury)
- [Conceptual Sketch](#sketch)
- [Ethereal](#ethereal)
- [Bohemian (Boho)](#bohemian)
- [Wabi-Sabi](#wabi-sabi)

---

### Scrapbook <a id="scrapbook"></a>
* **ID**: `scrapbook` (class `.theme-scrapbook`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Tactile collage: paper cut-outs, tape, stamps, hand-drawn notes, Polaroid frames, slightly rotated decorative elements.
* **Tokens**:
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
* **Ledger rows**: `scrapbook` in [contrast-ledger.md](contrast-ledger.md)

---

### Surrealism <a id="surrealism"></a>
* **ID**: `surrealism` (class `.theme-surrealism`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Dreamlike depth, floating objects, unexpected scale, atmospheric radial light.
* **Tokens**:
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
* **Ledger rows**: `surrealism` in [contrast-ledger.md](contrast-ledger.md)

---

### Luxury Typography <a id="luxury"></a>
* **ID**: `luxury` (class `.theme-luxury`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: High-contrast Didone serifs, hairline stems, wide tracking on short labels, monochrome restraint with gold ornament.
* **Tokens**:
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
* **Ledger rows**: `luxury` in [contrast-ledger.md](contrast-ledger.md)

---

### Conceptual Sketch <a id="sketch"></a>
* **ID**: `sketch` (class `.theme-sketch`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Hand-drawn wireframes, pencil outlines, graph-paper backdrop, wobbly borders, annotation arrows.
* **Tokens**:
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
* **Ledger rows**: `sketch` in [contrast-ledger.md](contrast-ledger.md)

---

### Ethereal <a id="ethereal"></a>
* **ID**: `ethereal` (class `.theme-ethereal`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Luminous ambient glow, soft pastel gradients, gentle diffusion, calm and light typography.
* **Tokens**:
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
* **Ledger rows**: `ethereal` in [contrast-ledger.md](contrast-ledger.md)

---

### Bohemian (Boho) <a id="bohemian"></a>
* **ID**: `bohemian` (class `.theme-bohemian`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Earthy terracotta and sage, botanical illustration, hand-crafted textures, sun-washed warmth.
* **Tokens**:
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
* **Ledger rows**: `bohemian` in [contrast-ledger.md](contrast-ledger.md)

---

### Wabi-Sabi <a id="wabi-sabi"></a>
* **ID**: `wabi-sabi` (class `.theme-wabi-sabi`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Japanese aesthetic of impermanence: asymmetric balance, raw textures (stone, clay, linen), quiet space.
* **Tokens**:
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
* **Ledger rows**: `wabi-sabi` in [contrast-ledger.md](contrast-ledger.md)
