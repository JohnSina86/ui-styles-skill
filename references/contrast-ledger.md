# Contrast ledger

Verified on **2026-10-01** with WCAG 2.x relative luminance. This file is the audit trail for the "contrast-verified" claim: every value below can be recomputed by hand or in a spreadsheet using the method at the end.

## Contents
- [Role pairs (every style)](#role-pairs-every-style)
- [Derived component and state pairs](#derived-component-and-state-pairs)
- [Method](#method)
- [Freshness rule](#freshness-rule)

## Role pairs (every style)
Needs: text pairs (`text`, `muted`, `on-accent`) >= 4.5:1; control and focus pairs (`border`, `focus`) >= 3:1.

| Style ID | text/bg | text/surface | muted/surface | muted/bg | on-accent/accent | border/surface | border/bg | focus/bg | focus/surface |
| :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| `claymorphism` | 13.73 | 11.44 | 6.79 | 8.14 | 5.70 | 4.26 | 5.11 | 8.23 | 6.85 |
| `cybercore` | 18.37 | 17.90 | 8.54 | 8.76 | 12.79 | 6.70 | 6.88 | 13.97 | 13.61 |
| `neo-brutalism` | 20.62 | 21.00 | 10.44 | 10.25 | 15.84 | 21.00 | 20.62 | 6.58 | 6.70 |
| `scrapbook` | 12.78 | 14.73 | 7.49 | 6.50 | 6.53 | 4.38 | 3.80 | 5.72 | 6.60 |
| `surrealism` | 17.26 | 13.52 | 8.34 | 10.64 | 10.60 | 4.48 | 5.72 | 11.10 | 8.70 |
| `y2k` | 15.00 | 15.99 | 8.18 | 7.67 | 6.00 | 4.02 | 3.77 | 5.57 | 5.93 |
| `pixel-art` | 12.48 | 19.00 | 11.92 | 7.83 | 17.28 | 19.00 | 12.48 | 5.55 | 8.46 |
| `synthwave` | 18.35 | 17.68 | 10.73 | 11.14 | 5.21 | 5.02 | 5.21 | 13.98 | 13.47 |
| `glassmorphism` | 17.85 | 7.95 | 5.35 | 12.02 | 8.33 | 3.10 | 6.96 | 10.71 | 4.77 |
| `neumorphism` | 11.60 | 11.60 | 5.97 | 5.97 | 5.67 | 3.36 | 3.36 | 5.29 | 5.29 |
| `bento-grid` | 16.97 | 17.72 | 7.73 | 7.41 | 6.29 | 4.83 | 4.63 | 6.02 | 6.29 |
| `editorial` | 16.20 | 17.07 | 7.63 | 7.24 | 7.31 | 17.07 | 16.20 | 6.94 | 7.31 |
| `swiss` | 21.00 | 21.00 | 10.37 | 10.37 | 5.70 | 21.00 | 21.00 | 10.69 | 10.69 |
| `minimalism` | 17.72 | 17.72 | 4.83 | 4.83 | 17.72 | 3.42 | 3.42 | 17.72 | 17.72 |
| `maximalism` | 19.24 | 16.93 | 12.96 | 14.72 | 16.57 | 13.36 | 15.18 | 14.86 | 13.08 |
| `luxury` | 17.92 | 19.67 | 9.47 | 8.63 | 17.92 | 5.64 | 5.14 | 17.92 | 19.67 |
| `sketch` | 13.49 | 13.97 | 7.46 | 7.20 | 6.70 | 13.97 | 13.49 | 5.00 | 5.18 |
| `ethereal` | 12.51 | 13.14 | 6.67 | 6.35 | 7.10 | 3.39 | 3.23 | 6.51 | 6.84 |
| `bohemian` | 9.07 | 9.77 | 6.22 | 5.77 | 6.11 | 4.22 | 3.92 | 5.36 | 5.77 |
| `victorian` | 11.32 | 12.73 | 8.29 | 7.37 | 12.73 | 12.73 | 11.32 | 11.22 | 12.62 |
| `cyberpunk` | 16.17 | 16.04 | 11.78 | 11.87 | 17.37 | 16.04 | 16.17 | 13.87 | 13.77 |
| `wabi-sabi` | 13.07 | 14.04 | 6.81 | 6.34 | 8.73 | 3.97 | 3.69 | 13.07 | 14.04 |

## Derived component and state pairs
Recipes in [styles-catalog.md](styles-catalog.md) cite these IDs. Glass pairs are computed over **pure white**, the worst-case backdrop.

| Row ID | Pair | Ratio | Needs |
| :--- | :--- | ---: | ---: |
| `D-glass-card-text` | Glass card text `#fff` over `rgba(15,23,42,.75)` composited on `#fff` | 7.95 | 4.5:1 |
| `D-glass-muted` | Glass muted text `#cbd5e1` on the same card | 5.35 | 4.5:1 |
| `D-glass-btn-rest` | Glass button label (`bg-white/12` = `rgba(255,255,255,.12)`) on card | 5.76 | 4.5:1 |
| `D-glass-btn-hover` | Glass button label hover (`hover:bg-white/20` = `rgba(255,255,255,.20)`) on card | 4.70 | 4.5:1 |
| `D-glass-focus-light` | Glass focus ring `#0f172a` on a white backdrop | 17.85 | 3.0:1 |
| `D-glass-focus-dark` | Glass inner ring `#ffffff` on a `#0f172a` backdrop | 17.85 | 3.0:1 |
| `D-cyber-card-text` | Cyberpunk card text `#fcee09` on `#0d0d11` | 16.04 | 4.5:1 |
| `D-cyber-btn-label` | Cyberpunk button label `#000` on `#fcee09` | 17.37 | 4.5:1 |
| `D-cyber-btn-hover` | Cyberpunk button label `#000` on hover `#00f0ff` | 14.91 | 4.5:1 |
| `D-cyber-focus` | Cyberpunk focus outline `#00f0ff` on `#0c0c0e` | 13.87 | 3.0:1 |
| `D-swiss-red-text` | Swiss text red `#d00000` on white | 5.70 | 4.5:1 |
| `D-swiss-red-pure` | Pure Swiss red `#ff0000` on white (**fails**: rules, blocks, text >= 24px only) | 4.00 | 3.0:1 |

`D-swiss-red-pure` is deliberately below the text threshold: it is a decorative-only colour, and its row exists so the failure stays visible.

## Method
1. Convert each sRGB channel to 0-1 and linearise: `c <= 0.04045 ? c/12.92 : ((c+0.055)/1.055)^2.4`.
2. `L = 0.2126 R + 0.7152 G + 0.0722 B`.
3. Ratio = `(L_lighter + 0.05) / (L_darker + 0.05)`.
4. For a translucent colour, composite first: `result = alpha * top + (1 - alpha) * under`, per channel, over the lightest backdrop it can sit on, then take the ratio.
5. Worked example (`D-glass-card-text`): `rgba(15,23,42,.75)` over `#fff` gives `rgb(75, 81, 95)` per channel (`0.75*15+0.25*255 = 75`, and so on). Linearised, that is (0.0704, 0.0823, 0.1144), so L = 0.2126*0.0704 + 0.7152*0.0823 + 0.0722*0.1144 = 0.0821. White has L = 1, so the ratio is 1.05 / 0.1321 = **7.95**.

## Freshness rule
Re-verify the affected rows when **any** of these changes: a token value, a recipe colour or alpha (CSS `rgba()` or a Tailwind utility such as `bg-white/12`) in `styles-catalog.md`, or the compositing assumption (the backdrop). Otherwise re-verify at least once a year. Update the "Verified on" date when you do.
