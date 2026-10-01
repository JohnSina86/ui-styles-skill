# Tokens: Retro & Nostalgic

Read this file **after** choosing a style from the SKILL.md style index. Every block contains only custom properties (see the token contract in SKILL.md). Colours were verified against WCAG 2.x: see [contrast-ledger.md](contrast-ledger.md).

## Contents
- [Y2K Aesthetic](#y2k)
- [Pixel Art](#pixel-art)
- [Synthwave](#synthwave)
- [Victorian](#victorian)

---

### Y2K Aesthetic <a id="y2k"></a>
* **ID**: `y2k` (class `.theme-y2k`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Early-2000s cyber-optimism: glossy candy buttons, chrome sheen, starbursts, bubble type, iridescence.
* **Tokens**:
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
* **Ledger rows**: `y2k` in [contrast-ledger.md](contrast-ledger.md)

---

### Pixel Art <a id="pixel-art"></a>
* **ID**: `pixel-art` (class `.theme-pixel-art`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: 8/16-bit arcade: visible raster grid, stepped block borders, bitmap fonts, restricted palette (PICO-8 here).
* **Tokens**:
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
* **Ledger rows**: `pixel-art` in [contrast-ledger.md](contrast-ledger.md)

---

### Synthwave <a id="synthwave"></a>
* **ID**: `synthwave` (class `.theme-synthwave`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: 1980s retrowave: neon magenta and cyan glows, perspective grids, neon sunsets, scanlines.
* **Tokens**:
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
* **Ledger rows**: `synthwave` in [contrast-ledger.md](contrast-ledger.md)

---

### Victorian <a id="victorian"></a>
* **ID**: `victorian` (class `.theme-victorian`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: 19th-century ornament: engraved filigree, double rules, jewel tones on parchment, decorative capitals.
* **Tokens**:
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
* **Ledger rows**: `victorian` in [contrast-ledger.md](contrast-ledger.md)
