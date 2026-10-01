# Tokens: Graphic & Modernist

Read this file **after** choosing a style from the SKILL.md style index. Every block contains only custom properties (see the token contract in SKILL.md). Colours were verified against WCAG 2.x: see [contrast-ledger.md](contrast-ledger.md).

## Contents
- [Neo-Brutalism](#neo-brutalism)
- [Bento Grid](#bento-grid)
- [Editorial Design](#editorial)
- [Swiss Design (International Typographic Style)](#swiss)
- [Minimalism](#minimalism)
- [Maximalism](#maximalism)

---

### Neo-Brutalism <a id="neo-brutalism"></a>
* **ID**: `neo-brutalism` (class `.theme-neo-brutalism`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Raw high contrast: thick black borders, hard offset shadows with zero blur, saturated colour blocks.
* **Tokens**:
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
* **Ledger rows**: `neo-brutalism` in [contrast-ledger.md](contrast-ledger.md)

---

### Bento Grid <a id="bento-grid"></a>
* **ID**: `bento-grid` (class `.theme-bento-grid`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Asymmetric modular grid of rounded cards, compact widgets, mixed spans.
* **Tokens**:
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
* **Ledger rows**: `bento-grid` in [contrast-ledger.md](contrast-ledger.md)

---

### Editorial Design <a id="editorial"></a>
* **ID**: `editorial` (class `.theme-editorial`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Magazine layout: dramatic serif headlines, multi-column text, pull quotes, drop caps, rules instead of shadows.
* **Tokens**:
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
* **Ledger rows**: `editorial` in [contrast-ledger.md](contrast-ledger.md)

---

### Swiss Design (International Typographic Style) <a id="swiss"></a>
* **ID**: `swiss` (class `.theme-swiss`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Strict mathematical grid, asymmetric balance, grotesque sans, single bold accent, no decoration.
* **Tokens**:
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
* **Ledger rows**: `swiss` in [contrast-ledger.md](contrast-ledger.md)

---

### Minimalism <a id="minimalism"></a>
* **ID**: `minimalism` (class `.theme-minimalism`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Intentional whitespace, removal of non-essential elements, content first.
* **Tokens**:
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
* **Ledger rows**: `minimalism` in [contrast-ledger.md](contrast-ledger.md)

---

### Maximalism <a id="maximalism"></a>
* **ID**: `maximalism` (class `.theme-maximalism`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Expressive abundance: dense layering, clashing patterns, saturated colour, kinetic type.
* **Tokens**:
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
* **Ledger rows**: `maximalism` in [contrast-ledger.md](contrast-ledger.md)
