# Tokens: High-Tech & Futuristic

Read this file **after** choosing a style from the SKILL.md style index. Every block contains only custom properties (see the token contract in SKILL.md). Colours were verified against WCAG 2.x: see [contrast-ledger.md](contrast-ledger.md).

## Contents
- [Cybercore](#cybercore)
- [Cyberpunk](#cyberpunk)

---

### Cybercore <a id="cybercore"></a>
* **ID**: `cybercore` (class `.theme-cybercore`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Technical wireframes, HUD overlays, coordinates, monospaced read-outs, thin geometric lines.
* **Tokens**:
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
* **Ledger rows**: `cybercore` in [contrast-ledger.md](contrast-ledger.md)

---

### Cyberpunk <a id="cyberpunk"></a>
* **ID**: `cyberpunk` (class `.theme-cyberpunk`). Aliases, fit and risk are in the SKILL.md style index.
* **Visual DNA**: Dystopian high-tech: angular cut corners, scanlines, high-voltage yellow and cyan on carbon.
* **Tokens**:
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
* **Ledger rows**: `cyberpunk` in [contrast-ledger.md](contrast-ledger.md)
