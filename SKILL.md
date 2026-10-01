---
name: ui-styles
description: >-
  Contrast-verified design tokens and CSS recipes for distinctive UI styles (Neo-Brutalism, Glassmorphism, Bento Grid, Cyberpunk, Swiss and more). Use when the user names a visual style or wants a distinctive theme for new UI, even without naming this skill. Not for UX critique (use ux-laws), WCAG audits, or restyling a project that already has a design system unless asked.
metadata:
  version: "1.2.1"
---

# UI Styles (v1.2)

Turns an aesthetic request into production CSS: one token block per style with fixed role names, verified contrast and shared guardrails. This file is the routing layer. Token blocks, recipes and CSS guardrails are in `references/`, and you read them **after** you choose a style.

## 0. Before you style (mandatory)
1. **Existing design system first.** If the project already has tokens, a theme file or a component library, don't replace it. Map the style onto the existing tokens as an accent layer, and only replace the system if the user asks.
2. **Detect Tailwind** (`package.json` -> `tailwindcss`) and read [tailwind-mapping.md](references/tailwind-mapping.md) if it is present.
3. **Font policy.** Check the project's CSP and asset policy. Prefer self-hosted fonts and never inject a remote font link by default (see [guardrails.md](references/guardrails.md), Fonts).
4. **Choose the style** using sections 1 and 2.

## 1. Style index (the selection source of truth)
Match the user's wording against **ID or Aliases**. `ux-laws #N` names the law in the companion skill that this style's risk most often touches. `Risk` tells you how much care a style needs, and `Requires` is the one rule that keeps it usable. `Tokens` names the file in `references/` (`tokens-<name>.md`) that holds the block, so read only that one.

| ID | Aliases | Best for | Avoid when | Risk | Requires | Tokens |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `claymorphism` | clay, soft 3D | games, education, onboarding | dense dashboards (ux-laws #4, #14) | medium | inputs get the 1px `--ui-border` | `dimensional` |
| `cybercore` | hud, wireframe | dev tools, terminals, telemetry | casual e-commerce (ux-laws #3) | medium | muted text stays >= `#8fb3bd` | `hightech` |
| `neo-brutalism` | neobrutalism, brutalism | SaaS marketing, portfolios, fintech for Gen-Z | conservative enterprise, healthcare (ux-laws #17) | low | none | `graphic` |
| `scrapbook` | collage, paper | creative portfolios, invitations, storytelling | efficiency workflows, funnels (ux-laws #12) | medium | no rotation on inputs or body text | `artistic` |
| `surrealism` | surreal, dreamlike | fashion, album releases, art showcases | utility apps, forms (ux-laws #3, #12) | medium | text only on solid panels | `artistic` |
| `y2k` | y2k aesthetic, chrome gloss | music, streetwear, youth entertainment | B2B, legal, finance | medium | text on `--ui-surface`, never on gradients | `retro` |
| `pixel-art` | 8-bit, retro game | retro gaming, indie dev hubs | long reading | high | pixel font for headings and labels only | `retro` |
| `synthwave` | retrowave, outrun | audio tools, streaming, night events | daytime reading, public services | medium | glow on headings >= 24px only | `retro` |
| `glassmorphism` | glass, frosted | control bars, OS-style panels, premium landing | text-heavy light backdrops (ux-laws #12, #17) | high | dark/saturated backdrop plus fallbacks | `dimensional` |
| `neumorphism` | soft ui, soft-ui | smart-home controls, synth dials | forms, state-critical UI (ux-laws #3, #13) | high | visible 1px control border | `dimensional` |
| `bento-grid` | bento | feature highlights, SaaS homepages | sequential content | low | inputs use `--ui-border`, not the card edge | `graphic` |
| `editorial` | magazine, long-form | journalism, essays, fashion stories | toolbars, data entry | low | single column on narrow screens | `graphic` |
| `swiss` | swiss design, international style | architecture, agencies, transit info | none structurally | low | text red is `#d00000`, not `#ff0000` | `graphic` |
| `minimalism` | minimal | writing tools, e-commerce, dev portfolios | icon-only controls, hairline inputs (ux-laws #3) | medium | inputs use `--ui-border`, not the hairline | `graphic` |
| `maximalism` | maximal | festivals, pop-culture magazines, drops | form-heavy transactions (ux-laws #1, #12) | high | patterns behind solid text panels only | `graphic` |
| `luxury` | luxury typography, didone | jewellery, real estate, fragrance, fine dining | fast dashboards | medium | gold is ornament only; tracking on labels only | `artistic` |
| `sketch` | conceptual sketch, blueprint | prototyping, planning, education | checkout flows (ux-laws #17) | medium | hand-drawn borders on decor, not on inputs | `artistic` |
| `ethereal` | dreamy, soft glow | meditation, wellness, skincare, journals | urgent consoles | medium | body weight >= 400 | `artistic` |
| `bohemian` | boho | artisan markets, eco goods, cafes | infrastructure consoles | low | mustard/terracotta are decor only | `artistic` |
| `victorian` | ornate, dark academia | heritage brands, escape rooms, archives | mobile utilities | medium | display font for headings only | `retro` |
| `cyberpunk` | cyber-punk | esports, sci-fi gaming, streaming | long reading (ux-laws #3) | medium | never clip the focusable element | `hightech` |
| `wabi-sabi` | wabi | studios, tea houses, ceramics, mindful reads | dense data views | low | none | `artistic` |

## 2. Choosing a style
- **The user named a style** (or an alias): use it. Mention its risk only if `Risk` is `high`.
- **The user named a product**: use [product-fit.md](references/product-fit.md). Propose a primary and a secondary style with one reason each, drawn from *Best for* and *Avoid when*. Never propose a style listed under Avoid for that product.
- **No product-fit row, but an indexed style fits:** proceed normally and say only that there is **no product-specific guidance** for the product type.
- **No indexed style fits:** say there is **no verified match**, offer the two closest styles labelled *unverified*, and never present them as catalog guidance.
- **Several styles can be combined** only if one is the base. Keep one `.theme-<id>` per container.

## 3. Token contract
Every style defines the same roles, so components never hard-code colours. A block contains **only custom properties**, and you apply it by adding `.theme-<id>` to `<html>` or any container.

| Token | Role |
| :--- | :--- |
| `--ui-bg`, `--ui-surface` | Page background; cards, panels, inputs |
| `--ui-text`, `--ui-text-muted` | Body and secondary text |
| `--ui-accent`, `--ui-on-accent` | Primary action fill and its label |
| `--ui-border` | Boundary of controls (inputs, toggles, outline buttons) |
| `--ui-focus` | Focus indicator |
| `--ui-radius`, `--ui-shadow` | Shape and elevation |
| `--ui-font-display`, `--ui-font-body` | Font stacks with generic fallbacks |

Some styles add optional properties (`--ui-border-width`, `--ui-blur`, `--ui-backdrop`, `--ui-tilt`, `--ui-chrome`, `--ui-pattern`, `--ui-tracking`, `--ui-leading`). Components consume them.

## 4. Contrast contract
Text, muted text and on-accent pairs are >= 4.5:1, and border and focus pairs are >= 3:1. Every role pair and every derived component or state pair (glass tint, button hover, Cyberpunk labels) is recorded in [contrast-ledger.md](references/contrast-ledger.md) with the method. A colour listed under *Decorative only* fails at least one threshold, so use it **only for ornament and rules**. It may carry large text (>= 24px, or >= 18.66px bold) only if a ledger row for that exact colour and backdrop shows >= 3:1. **If you change a token or a recipe colour or alpha, recompute the ratio and update the ledger.** Don't judge contrast by eye.

## 5. Guardrails (full CSS in [guardrails.md](references/guardrails.md))
- **Focus:** a visible `:focus-visible` outline on every interactive element. Never put `clip-path`, `mask` or `overflow: hidden` on a focusable element.
- **Motion:** honour `prefers-reduced-motion`. Mark decorative transforms with `data-ui-motion`.
- **Transparency:** provide an `@supports` fallback and honour `prefers-reduced-transparency`. Glass is used only over a dark or saturated backdrop, and the surface tint must not be lowered.
- **Forced colours:** controls drawn only with backgrounds or pseudo-elements need a real border in `@media (forced-colors: active)`.
- **Fonts:** self-host by default, end every stack in a generic family, and quote family names exactly once (`"Press Start 2P"`).
- **Dark mode:** redefine the same roles under a selector and re-run the contrast check. Dark-only styles stay dark-only.

## 6. Workflow
1. Do section 0, then choose with sections 1 and 2. If the user only asks you to pick, recommend or explain a style, answer with the recommendation, the reasons and the risk, and don't write CSS or token files unless they ask.
2. Read `references/tokens-<name>.md` and paste the style's block into the global stylesheet. Add the Tailwind mapping if needed, and the guardrails once.
3. Build components from roles. For Neo-Brutalism, Glassmorphism, Bento Grid, Cyberpunk, Swiss and Wabi-Sabi use [styles-catalog.md](references/styles-catalog.md). For any other style, use this pattern, **scoped to the theme** (if the project already has card, button or input components, map the roles into *those* selectors instead):
   ```css
   :where([class*="theme-"]) { font-family: var(--ui-font-body); }
   :where([class*="theme-"]) :is(h1, h2, h3, h4) { font-family: var(--ui-font-display); }
   :where([class*="theme-"]) .ui-card { background: var(--ui-surface); color: var(--ui-text); border-radius: var(--ui-radius); box-shadow: var(--ui-shadow); padding: 24px; }
   :where([class*="theme-"]) .ui-button { background: var(--ui-accent); color: var(--ui-on-accent); border: 2px solid transparent; border-radius: var(--ui-radius); min-height: 44px; padding: 10px 20px; font-family: var(--ui-font-display); }
   :where([class*="theme-"]) .ui-input { background: var(--ui-surface); color: var(--ui-text); border: 1px solid var(--ui-border); border-radius: var(--ui-radius); min-height: 44px; padding: 8px 12px; }
   ```
4. Run the checklist in section 7.
5. If the user asks for ready-made or animated components, icons, fonts, charts or companion skills, read [related-resources.md](references/related-resources.md) first and follow its rules. Never recreate a library's component or icon from memory.
6. For a UX review of the result, use `ux-laws`. It grades structure and behaviour, not the chosen aesthetic.

## 7. Pre-delivery checklist
- [ ] Existing design system respected (section 0).
- [ ] Style chosen from the index or product-fit table, with the risk and `Requires` rule applied.
- [ ] Only `--ui-*` roles used; no hard-coded colours outside decorative uses. A badge or tag colour that isn't in the ledger is decorative only, and its text uses a ledger on-colour.
- [ ] Headings follow a logical order with no skipped levels, whatever the display font.
- [ ] Every text, control and focus pair is in the ledger (or was recomputed).
- [ ] Visible focus on every interactive element, and no clipped focusable element.
- [ ] Reduced motion, reduced transparency and forced colours handled.
- [ ] Target size: aim for 44x44 on touch-first surfaces. Before reporting a WCAG 2.2 AA 2.5.8 failure for a target under 24x24 CSS px, check the spacing test **and** the exceptions (inline in text, equivalent control elsewhere, user-agent default, essential). The `ux-laws` skill has the full procedure.
- [ ] No emoji used as icons; fonts self-hosted or policy-approved, with generic fallbacks.
- [ ] Layout checked at narrow width and 200% zoom, with text reflowing without clipping.

## References
- [styles-catalog.md](references/styles-catalog.md): card, button and input recipes for six styles.
- [product-fit.md](references/product-fit.md): product type to style table.
- [contrast-ledger.md](references/contrast-ledger.md): verified ratios and method.
- [related-resources.md](references/related-resources.md): links to third-party components, icons, fonts, motion, charts and companion skills, and the rules for using them.
- [source-scorecard.md](references/source-scorecard.md): how those links were scored, and their limits.
- [guardrails.md](references/guardrails.md): focus, motion, transparency, forced colours, fonts and dark-mode CSS.
- [tailwind-mapping.md](references/tailwind-mapping.md): v4 and v3 mappings.
- Token blocks: [dimensional](references/tokens-dimensional.md), [graphic](references/tokens-graphic.md), [retro](references/tokens-retro.md), [hightech](references/tokens-hightech.md), [artistic](references/tokens-artistic.md).
