# Tokens: Dimensional & Tactile

Read this file **after** choosing a style from the SKILL.md style index. Every block contains only custom properties (see the token contract in SKILL.md). Colours were verified against WCAG 2.x: see [contrast-ledger.md](contrast-ledger.md).

## Contents
- [Claymorphism](#claymorphism)
- [Glassmorphism](#glassmorphism)
- [Neumorphism (Soft UI)](#neumorphism)

---

### Claymorphism <a id="claymorphism"></a>
* **ID**: `claymorphism` (class `.theme-claymorphism`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Puffy, inflated clay shapes: pastel surfaces with outer shadows tinted from the surface colour plus soft inner highlights. Friendly and tactile.
* **Tokens**:
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
* **Ledger rows**: `claymorphism` in [contrast-ledger.md](contrast-ledger.md)

---

### Glassmorphism <a id="glassmorphism"></a>
* **ID**: `glassmorphism` (class `.theme-glassmorphism`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Frosted translucent panels with backdrop blur over a dark or saturated backdrop, hairline specular edges.
* **Tokens**:
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
* **Ledger rows**: `glassmorphism` in [contrast-ledger.md](contrast-ledger.md)

---

### Neumorphism (Soft UI) <a id="neumorphism"></a>
* **ID**: `neumorphism` (class `.theme-neumorphism`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Extruded-plastic surfaces that look sculpted from the background; monochrome.
* **Tokens**:
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
* **Ledger rows**: `neumorphism` in [contrast-ledger.md](contrast-ledger.md)
