# Composition moves

Three layout moves that work under any style. They add no colours and no roles: they arrange the tokens a style already has. Use them when a screen feels flat, looks like a default template, or users can't tell what to tap.

They are craft heuristics, not graded rules. `ux-laws` grades the result, never whether a move was used. The nearest evidence is `ux-laws` law 7 (Von Restorff) and law 12 (Prägnanz). **Source:** adapted from a short creator tip (Instagram, @ayoships, 2026), rewritten in this skill's terms and bounded by its contracts. It is not research.

## Contents
- [When to use which](#when-to-use-which)
- [1. Depth planes](#1-depth-planes)
- [2. Signal colour](#2-signal-colour)
- [3. Scale contrast](#3-scale-contrast)
- [Checks](#checks)

## When to use which
| Symptom | Move | Good on | Skip on |
| :--- | :--- | :--- | :--- |
| Flat: nothing has depth | Depth planes | hero, product detail, profile, landing, onboarding | dense dashboards, forms, tables, long reading |
| Users can't tell what to tap | Signal colour | every surface | none |
| Looks default or templated | Scale contrast | landing, product detail, profile, editorial | dashboards and data views, which need middle sizes to rank data |

Section 0 still applies: in an existing design system, propose a move and apply it only if the user agrees. A style's `Requires` rule wins over a move. For example, `surrealism` and `y2k` keep text on solid panels, so the depth planes' back type there is decoration only.

## 1. Depth planes
Stack the screen in three planes, back to front:
- **Back:** one oversized word or number (brand, name, price) in `--ui-font-display`. It is decoration.
- **Middle:** the subject (product cut-out, portrait, illustration). It may overlap the back type.
- **Front:** controls and readable text. Nothing overlaps them.

```css
:where([class*="theme-"]) .ui-stage { display: grid; isolation: isolate; }
:where([class*="theme-"]) .ui-stage > * { grid-area: 1 / 1; }
:where([class*="theme-"]) .ui-plane-back { z-index: 0; overflow: clip; font-family: var(--ui-font-display); font-size: clamp(4rem, 22vw, 12rem); line-height: 0.85; color: var(--ui-text); }
:where([class*="theme-"]) .ui-plane-mid { z-index: 1; pointer-events: none; }
:where([class*="theme-"]) .ui-plane-front { z-index: 2; align-self: end; }
```
```html
<div class="ui-stage">
  <p class="ui-plane-back" aria-hidden="true">AURA</p>
  <img class="ui-plane-mid" src="headphones.png" alt="Aura Studio headphones in sage green">
  <div class="ui-plane-front"><h1>Aura Studio</h1> … <button type="button" class="ui-button">Add to bag</button></div>
</div>
```
- **The back word is decorative.** Give it `aria-hidden="true"` and make sure the same words exist as real text in the front plane. If the word must be read, it counts as large text and needs >= 3:1 at every backdrop it crosses (contrast contract). Over a photo that is rarely provable, so keep it decorative.
- **Never in the signal colour.** The back word uses `--ui-text`, `--ui-text-muted` or a decorative-only colour, never `--ui-accent` (move 2).
- **The subject never covers a control.** A transparent image still takes clicks inside its box, so it gets `pointer-events: none`. Confirm the front plane's hit areas with the `ux-laws` hit-testing method when a page can be rendered.
- **Clip the word, not the controls.** `overflow: clip` goes on the back plane only, never on a focusable element or the front plane (focus guardrail). Check for horizontal overflow at narrow width.
- **Motion:** parallax or drift on a plane is decorative. Mark it `data-ui-motion` (motion guardrail).

## 2. Signal colour
One colour means "you can act here", and nothing else uses it. In the token contract that colour is `--ui-accent` with `--ui-on-accent`. Everything else is ink and paper: `--ui-text`, `--ui-text-muted`, `--ui-surface`, `--ui-bg`, `--ui-border`.
- **Accent only on interactive things and their states:** primary buttons, links, the selected or active state of a control. `--ui-focus` may share the colour.
- **Never on decoration:** headings, prices, badges, illustrations, icons that do nothing, back-plane type. A token block or recipe that uses the accent decoratively (the Synthwave heading glow) drops that use while this move is on. If the style can't hold without it, tell the user they clash.
- **Secondary actions get no second colour.** Use an outline (`--ui-border`) or ink text. Keep one accent-filled action per region, so the primary stays distinct (`ux-laws` law 7).
- **Accent as text is a new pair.** A link in `--ui-accent` on `--ui-bg` or `--ui-surface` is not the `--ui-on-accent` row. Find its ledger row or recompute it: >= 4.5:1 for text, >= 3:1 for a control boundary.
- **Not colour alone.** Interactive things also look interactive: button shape, underlined links in running text.
- **Decor palettes keep their decor.** Styles such as `maximalism`, `bohemian` or `synthwave` keep their decorative colours, but no decoration uses the accent hue.
- **Status colours stay separate.** Error and success keep their own colours with an icon or text. If the accent and the error colour are the same hue, the error state must not rely on colour.

**Quick check:** search the delivered CSS for `--ui-accent` (and the Tailwind `ui-accent` utilities). Every selector it appears in is an interactive element or one of its states.

## 3. Scale contrast
Make one thing huge and everything else small, with no middle sizes on that view.
- **Choose the one thing.** It is usually the name, number or price that the user's main task hinges on. Only one per view: two huge things compete (`ux-laws` law 7).
- **Two sizes and a floor:** display `clamp(3rem, 12vw, 8rem)` for the one thing, body `1rem`, labels and meta `0.8125rem` to `0.875rem`. Leave out the 20 to 40px band. Rank the rest with weight, case, tracking (`--ui-tracking` where the style has it) and `--ui-text-muted`, not size.
- **Floors:** reading text is never below 16px, and labels never below 12px. "Tiny" means smaller than the display, not unreadable.
- **Semantics don't follow size.** Heading levels follow document order (pre-delivery checklist), so a small `h2` is fine.
- **Huge text must reflow.** Use `clamp()` with a `vw` term, allow long names to break (`overflow-wrap: anywhere`), and check 320px width and 200% zoom.

## Checks
Add these to the section 7 checklist for each move you used.
- [ ] **Depth planes:** back word `aria-hidden` with real text elsewhere, or its contrast recomputed at every backdrop. Subject has `pointer-events: none`. No control or body text is overlapped. No clipped focusable element. No horizontal overflow at narrow width.
- [ ] **Signal colour:** every `--ui-accent` use is an interactive element or its state. Accent text pairs are in the ledger or recomputed. Secondary actions don't use a second colour.
- [ ] **Scale contrast:** one huge element per view. Body >= 16px and labels >= 12px. Heading order is logical. Reflow checked at 320px and 200% zoom, or left open as "needs a render".
