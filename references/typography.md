# Typography and rhythm

The type scale, measure, spacing scale and vertical rhythm that make a page read as designed rather than defaulted, plus which display face pairs with which body face for every style. It extends the **scale contrast** move in [composition.md](composition.md) (section 3) and adds no colours: the contrast contract, the style's `Requires` rule and the guardrails still win. All faces come from the style's own token block; this file adds no fonts.

These are craft heuristics, not graded rules. `ux-laws` grades legibility and hierarchy, never whether this scale was used.

## Contents
- [1. Two-step type scale](#1-two-step-type-scale)
- [2. Measure](#2-measure)
- [3. Spacing scale](#3-spacing-scale)
- [4. Vertical rhythm](#4-vertical-rhythm)
- [5. Pairing table](#5-pairing-table)
- [Checks](#checks)

## 1. Two-step type scale
Each view (the first screen, then each section) has **one huge element** and everything else is body or meta. Nothing sits in the 20 to 40px band within a view.

| Step | Size | Used for |
| :--- | :--- | :--- |
| Display | `clamp(3rem, 12vw, 8rem)` on the first screen; `clamp(2rem, 6vw, 4rem)` for a section's huge element | the name, number, price or heading the view hinges on, in `--ui-font-display` |
| Body | `1rem` (long reading pages may use `1.125rem`) | paragraphs, list items, control labels, in `--ui-font-body` |
| Meta | `0.8125rem` to `0.875rem` | labels, captions, timestamps, eyebrows, in `--ui-text-muted` or with weight, case and tracking |

- **Floors:** reading text is never below 16px and labels never below 12px. A pairing note below may raise a floor for a face with a small x-height.
- **The `vw` term is mandatory** on the display step so the huge element reflows. Add `overflow-wrap: anywhere` and check 320px and 200% zoom.
- **Rank without size.** A section heading that is not the section's huge element is body-sized in the display face, ranked by weight, case and `--ui-tracking` where the style has it. Heading levels still follow document order (pre-delivery checklist).
- **One huge element per view.** Two compete (`ux-laws` law 7). A section may have none.

```css
:where([class*="theme-"]) .ui-display { font-family: var(--ui-font-display); font-size: clamp(3rem, 12vw, 8rem); line-height: 1; overflow-wrap: anywhere; }
:where([class*="theme-"]) .ui-display-section { font-family: var(--ui-font-display); font-size: clamp(2rem, 6vw, 4rem); line-height: 1.05; overflow-wrap: anywhere; }
:where([class*="theme-"]) .ui-body { font-family: var(--ui-font-body); font-size: 1rem; line-height: var(--ui-leading, 1.55); max-inline-size: 65ch; }
:where([class*="theme-"]) .ui-meta { font-size: 0.875rem; line-height: 1.4; color: var(--ui-text-muted); letter-spacing: var(--ui-tracking, 0.02em); }
```

## 2. Measure
Reading text (paragraphs, bios, descriptions, article body) sits in a column of **45 to 75 characters**: `max-inline-size: 65ch` on the text block or its column. The `ch` unit follows the body face, so the rule holds when the font changes.
- The cap is the rule. Below about 420px the column is narrower than 45 characters; keep the body size and let the measure fall, never shrink text to fit more per line.
- Headings, labels and controls are exempt. Card text follows the rule inside the card: a card wider than 75 characters needs an inner cap or a second column.
- Line height follows the measure: 1.5 to 1.6 for body at 65 characters, tighter (1.3 to 1.4) for meta, 1 to 1.1 for display. A style's `--ui-leading` wins where it has one.

## 3. Spacing scale
Six optional roles, listed in the token contract as optional properties. Components consume them, so no new component carries a hard-coded padding once a style defines them. The default block fits every style; two variants change only the top step.

```css
:where([class*="theme-"]) {
  --ui-space-1: 0.25rem;  /* 4px: icon gaps, inline padding */
  --ui-space-2: 0.5rem;   /* 8px: label to control, chip padding */
  --ui-space-3: 1rem;     /* 16px: paragraph gap, card padding on phones */
  --ui-space-4: 1.5rem;   /* 24px: card padding (the catalog's 24px), grid gap */
  --ui-space-5: 2.5rem;   /* 40px: between groups inside a section */
  --ui-space-6: clamp(3rem, 8vw, 6rem);  /* 48 to 96px: section padding */
}
/* airy: editorial, ethereal, luxury, minimalism, wabi-sabi */
.theme-editorial, .theme-ethereal, .theme-luxury, .theme-minimalism, .theme-wabi-sabi { --ui-space-6: clamp(4rem, 12vw, 9rem); }
/* dense: bento-grid, cybercore, pixel-art */
.theme-bento-grid, .theme-cybercore, .theme-pixel-art { --ui-space-6: clamp(2rem, 6vw, 4rem); }
```
Four steps (`1`, `3`, `4`, `6`) are enough for a small component set; use all six on a page. Never add a seventh: a value that isn't on the scale is a hard-coded padding.

## 4. Vertical rhythm
Section padding varies by the section's role. **Never one value top to bottom:** a page whose every section has the same `padding-block` reads as a template whatever the style.

| Section role | Block padding | Inside the section |
| :--- | :--- | :--- |
| Hero (first screen) | `--ui-space-6` top and bottom | `--ui-space-4` between heading, body and controls |
| Content section | `--ui-space-6` top, `--ui-space-5` bottom | `--ui-space-5` between groups, `--ui-space-3` between paragraphs |
| Band (one quote, one number or one call to action, on its own surface) | `--ui-space-5` top and bottom | nothing else in it |
| Footer | `--ui-space-5` top, `--ui-space-4` bottom | `--ui-space-2` between links |

- **Space before a heading is larger than the space after it**, so the heading binds to what follows: `margin-block: var(--ui-space-5) var(--ui-space-3)`, reset on the first child.
- **Use `gap` or the parent's padding**, not margins on children, so nothing collapses unpredictably and the rhythm survives a reorder.
- **Adjacent sections don't add margin.** The padding is the rhythm; a margin between sections doubles it.
- **Phones:** the `vw` term in `--ui-space-6` shrinks section padding; the `clamp()` floor keeps a hero from touching the next section.

## 5. Pairing table
One row per style ID in the SKILL.md index, in index order. Both faces are the style's own `--ui-font-display` and `--ui-font-body` stacks; where they are the same family the pairing is **one family**, ranked by weight and size, never a second font. The notes are floors and limits for that face; the style's `Requires` rule still applies.

| ID | Display face (weight) | Body face (weight) | Notes |
| :--- | :--- | :--- | :--- |
| `claymorphism` | Nunito 800 | Nunito 400 | One family. Meta at 600, not lighter, so it stays soft without going faint. |
| `cybercore` | JetBrains Mono 700 | JetBrains Mono 400 | One family. Cap the display at `6rem`: mono is wide. Read-outs and coordinates are the meta step. |
| `neo-brutalism` | Space Grotesk 700 | Space Grotesk 400 | One family. Display at line height 0.95; the border and offset shadow do the rest. |
| `scrapbook` | Caveat 700 | Lora 400 | Caveat on headings and short notes only, never below 24px. Body never rotated. |
| `surrealism` | Syne 800 | Inter 400 | Syne at 800 only; lighter weights lose the shape. Text on solid panels only. |
| `y2k` | Outfit 800 | Outfit 400 | One family. Display may take `-0.02em` tracking. Text on `--ui-surface`, never on the chrome gradient. |
| `pixel-art` | Press Start 2P | VT323 | Set Press Start 2P at multiples of 8px (16, 24, 32) so pixels align, display cap `4rem`. VT323 body floor `1.25rem`: its x-height is small. Headings and labels only in Press Start 2P. |
| `synthwave` | Orbitron 700 | Inter 400 | Orbitron on headings only; glow at 24px and above only. Meta in Inter. |
| `glassmorphism` | Inter 700 | Inter 400 | One family. Display at `-0.02em`; the glass edge, not a second face, separates panels. |
| `neumorphism` | Inter 600 | Inter 400 | One family. Keep display at 600: the style is low-contrast, so size does the ranking. |
| `bento-grid` | Plus Jakarta Sans 700 | Inter 400 | Plus Jakarta Sans for the one huge number or title per card; Inter for everything else. |
| `editorial` | Playfair Display 700 | Newsreader 400 | Playfair italic for pull quotes. Body `1.125rem` on long reads, measure 65 characters. |
| `swiss` | Inter 800 | Inter 400 | One family. Display uppercase at `-0.03em`; body sentence case. The grid ranks, not a second face. |
| `minimalism` | Inter 500 | Inter 400 | One family. Display stays at 500; size does all the work. Meta in `--ui-text-muted`. |
| `maximalism` | Anton | Inter 400 | Anton uppercase at line height 0.9, display only, never below 24px and never on labels. |
| `luxury` | Bodoni Moda 400 | Cormorant Garamond 400 | Bodoni hairlines need size: display floor `3rem`, never bold. Cormorant body floor `1.125rem`. Tracking on labels only. |
| `sketch` | Architects Daughter | Inter 400 | Architects Daughter for headings and annotations at 20px and above; labels and inputs in Inter. |
| `ethereal` | Cormorant Garamond 500 | Urbanist 400 | Cormorant display floor `2.5rem`. Body weight 400 or more. Meta in Urbanist. |
| `bohemian` | Fraunces 600 | Lora 400 | Fraunces at optical size for display; labels in Lora, not Fraunces. |
| `victorian` | Cinzel Decorative | Lora 400 | Cinzel Decorative is capitals only: headings only, never below 24px, never on labels. Lora for labels. |
| `cyberpunk` | Rajdhani 700 | Chakra Petch 400 | Rajdhani uppercase for display; Chakra Petch body `1rem`, labels 12px and above. No long reading. |
| `wabi-sabi` | Shippori Mincho 500 | Cormorant Garamond 400 | Body uses `--ui-leading` 1.8 and `--ui-tracking`. Cormorant body floor `1.125rem`. |

## Checks
Add these to the section 7 checklist when you set the type scale.
- [ ] **Scale:** one huge element per view, set with `clamp()` and a `vw` term; nothing in the 20 to 40px band within a view. Reading text >= 16px, labels >= 12px, plus any face floor from the pairing table.
- [ ] **Measure:** reading text capped at 45 to 75 characters (`ch`), text not shrunk to fit on phones.
- [ ] **Spacing:** every padding and gap is a `--ui-space-*` step; at least two different section paddings on the page.
- [ ] **Pairing:** the display and body faces are the row's faces from the style's token block, with the row's weights and floors. No font added.
- [ ] **Reflow:** 320px and 200% zoom checked, or left open as "needs a render".
