# UI Styles & Visual Themes AI Skill (`ui-styles`)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skill: Agents](https://img.shields.io/badge/Skill-Claude%20Code%20%2F%20Antigravity-purple.svg)](SKILL.md)

An agent skill with **contrast-verified design tokens and CSS/Tailwind recipes for 22 distinctive UI styles**. It's designed for AI coding assistants (Claude Code, Google Antigravity, Cursor, Copilot), so they produce coherent, accessible themes instead of generic grey-box templates.

## What's inside

- **One token block per style** with fixed role names (`--ui-bg`, `--ui-surface`, `--ui-text`, `--ui-accent`, `--ui-border`, `--ui-focus`, …), so components never hard-code colours.
- **Every text and control colour pair is computed against WCAG 2.x.** Colours that fail are marked *decorative only*.
- **Tailwind mappings** for v4 (`@theme inline`) and v3 (`theme.extend`).
- **Shared guardrails:** visible focus, `prefers-reduced-motion`, `prefers-reduced-transparency`, a `backdrop-filter` fallback, self-hosted font loading and dark-mode notes.
- **Detailed component recipes** (card, button, input) for six styles in [`references/styles-catalog.md`](references/styles-catalog.md). The others are built from their tokens using the shared role pattern.
- **Composition moves** ([`references/composition.md`](references/composition.md)): depth planes, a single signal colour and extreme scale contrast, for screens that feel flat or default. They work under any style and keep its contracts.
- **Anti-slop tells** ([`references/anti-slop.md`](references/anti-slop.md)): a frozen rubric of about twenty tells of a default AI-generated page (centred hero stack, icon-card grid, purple-blue gradient, fake logo rows, gradient text and more), each with a severity, a fix in the skill's own vocabulary, an applicability exception, the evidence required and a counting unit, plus a five-question "Could this be any site?" test. Prevalence observations, not detection.
- **Typography and imagery** ([`references/typography.md`](references/typography.md), [`references/imagery.md`](references/imagery.md)): a two-step type scale with 16px and 12px floors, a 45 to 75 character measure, an optional `--ui-space-*` spacing scale, section padding that varies by role, and a display-and-body pairing for every style from its own font stack; plus the imagery kind per style (photo, illustration, 3D, typographic or none), treatment rules, a ban list and an imagery note per product-fit row.
- **Reveal choreography** ([`references/choreography.md`](references/choreography.md)): the order a first screen arrives in (loader or none, a gate, staggered type, the subject last), a timing budget, what never moves (controls and body text), a static reduced-motion end state and one framework-free CSS example.
- **A style index** in `SKILL.md` with aliases, *Best for*, *Avoid when*, a risk flag and the one rule that keeps each style usable, plus a hand-written [product-fit table](references/product-fit.md).
- **A contrast ledger** ([`references/contrast-ledger.md`](references/contrast-ledger.md)) with every role pair and every derived component pair, the method, and a freshness rule. A copy-paste [contrast check](references/contrast-check.md) computes any pair by the same method and prints both luminances.
- **Related resources** ([`references/related-resources.md`](references/related-resources.md)): links, not bundled code, for components, icons, fonts, motion, charts and companion agent skills, chosen by a scored comparison ([`references/source-scorecard.md`](references/source-scorecard.md)), plus rules for using them (licence check, no invented URLs, no run-time remote rules, one icon family per project, tokens and reduced motion still apply). The scores are reported, not independently verified.
- **Evals** in [`evals/`](evals/): nine functional tasks and twenty trigger queries (half are near-miss negatives).
- **A runnable demo:** [`examples/cyberpunk-glass.html`](examples/cyberpunk-glass.html).

## The 22 styles

| Archetype | Styles |
| :--- | :--- |
| Dimensional & Tactile | Claymorphism, Neumorphism, Glassmorphism |
| Graphic & Modernist | Neo-Brutalism, Swiss Design, Minimalism, Maximalism, Editorial Design, Bento Grid |
| Retro & Nostalgic | Y2K Aesthetic, Pixel Art, Synthwave, Victorian |
| High-Tech & Futuristic | Cybercore, Cyberpunk |
| Artistic & Organic | Scrapbook, Surrealism, Conceptual Sketch, Ethereal, Bohemian, Luxury Typography, Wabi-Sabi |

The style index in [`SKILL.md`](SKILL.md) lists each style's aliases, *Best for*, *Avoid when* and risk. Its tokens, visual DNA and decorative-only colours are in `references/tokens-<archetype>.md`. The *Avoid when* lines point to the relevant law in the companion [ux-laws skill](https://github.com/JohnSina86/ux-laws-skill).

## Installation

Install a tagged release, so you get a reviewed version and not whatever the default branch holds later.

> **Current release: `v1.3.0`.** To confirm an install, run `git -C <install dir> describe --tags`, which should print `v1.3.0`.

### Claude Code
User level, so the skill is available in every project:
```bash
mkdir -p ~/.claude/skills && git clone --branch v1.3.0 https://github.com/JohnSina86/ui-styles-skill.git ~/.claude/skills/ui-styles
```
```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null; git clone --branch v1.3.0 https://github.com/JohnSina86/ui-styles-skill.git "$HOME\.claude\skills\ui-styles"
```
For project level, run this from the project root:
```bash
mkdir -p .claude/skills && git clone --branch v1.3.0 https://github.com/JohnSina86/ui-styles-skill.git .claude/skills/ui-styles
```
```powershell
New-Item -ItemType Directory -Force ".claude\skills" | Out-Null; git clone --branch v1.3.0 https://github.com/JohnSina86/ui-styles-skill.git ".claude\skills\ui-styles"
```
The folder name must be `ui-styles`, which is the skill's `name`. Claude Code loads the skill on demand from its description, so you don't need to edit a system prompt.

### Google Antigravity
```bash
mkdir -p .agents/skills && git clone --branch v1.3.0 https://github.com/JohnSina86/ui-styles-skill.git .agents/skills/ui-styles          # project
mkdir -p ~/.gemini/config/skills && git clone --branch v1.3.0 https://github.com/JohnSina86/ui-styles-skill.git ~/.gemini/config/skills/ui-styles   # global
```

### Cursor, Copilot and other tools without native skills
Clone it as above, then reference it in your rules file:
```markdown
When designing or building UI components, follow .agents/skills/ui-styles/SKILL.md (tokens, contrast notes and guardrails).
```

## Example prompts

- "Build a hero section and pricing card in Neo-Brutalism using Tailwind v4."
- "Add a Glassmorphism control bar to this dashboard, mapped onto our existing tokens."
- "Create an artisan coffee homepage in the Bohemian style, with self-hosted fonts."

## Changelog

- **v1.8.0**
  - `references/anti-slop.md`: rubric v1.5, 23 rows (was 21). A blind look score (Codex GPT-6 Astra) rated five client proposals that all passed v1.4 with zero tells at 30, 39, 48, 75 and 86 out of 100, so six predicates were widened and two rows added; the gate is unchanged. `purple-blue-gradient` also counts a pastel mesh (mist, blush, mint) behind a saturated violet accent; `uniform-soft-cards` counts two cards, not four; `icon-card-grid` counts three or more equal cards with or without icons, and placeholder slots are not real items; `interchangeable-copy` counts a headline that is only a category plus an audience pair, unless the brief supplied nothing more and the page marks the missing claim as pending; new `pill-chrome` (pill primary buttons, rounded status chips, skeleton bars) and `italic-serif-emphasis` (serif headlines with some words italic). `ethereal`'s documented tokens, `glassmorphism` recipes and requested comparison layouts stay exempt. Recalibrated against the five proposals from source: the two that scored 75 and 86 no longer pass, the two that scored 39 and 30 still do.
  - `SKILL.md` description also triggers on a request that calls a UI generic or AI-made. Eval 7 expects the widened `icon-card-grid` predicate.

- **v1.7.0**
  - `references/choreography.md`: how a first-screen reveal arrives. The order (loader or none, a gate that holds content while the loader is up, staggered headings and decoration, the hero subject last), a timing budget (everything at rest under 1.2 s, steps of 40 to 80 ms from `--ui-stagger`, nothing starting after 600 ms), what never moves (controls and body text appear at rest), a static end state under reduced motion, one choreographed section per view above the fold with only inview reveals below it, and `data-ui-reveal` on every choreographed element beside the shared `data-ui-motion` marker. One scoped CSS example using transforms and `clip-path` at full opacity. Workflow step 7, a checklist line and eval 9 point to it; a page with no reveal records `choreography: none`. Rewritten framework-free from Textura's public-domain [`next16-claude-starter`](https://github.com/textura-agency/next16-claude-starter) (its animation system, motion rules and fix catalogue).
  - **Eval 9, hand-run once on the final text:** 13 of 13 expectations pass (order; budget; controls and body text at rest; no first-screen fade; reduced-motion end state; `data-ui-reveal` count matching the choreography line; loader hidden without script and exiting by clip; scroll restoration kept on reload, history and fragment navigation; deadline at gate time with one terminal cleanup; the hero image's box reserved and its decode in the gate; gate selectors that match the theme class on `<html>` or on a wrapper; keyboard focus dismissing the loader; render items left open). **Limits:** run by a subagent that inherited the other installed user-level skills (none invoked), so not isolated to this skill, and with no browser, so the output was graded by reading its files, not by watching it play. Four earlier runs on drafts of this file are recorded in the pull request. **Known deviation:** the 1.2 s budget covers the reveal after the loader lifts; the wait before it is bounded separately by the 3 s deadline, not by the budget.
- **v1.6.0**
  - `references/typography.md`: a two-step type scale that extends the scale-contrast move on the views that move allows (display via `clamp()` with a `vw` term, body `1rem`, meta `0.8125rem` to `0.875rem`, floors of 16px for reading text and 12px for labels), a measure of 45 to 75 characters, six optional `--ui-space-*` steps added to the token contract, section padding by role on pages (never one value top to bottom), and a pairing table that names the display and body face for every style from its existing stack. No fonts added; the style index is unchanged.
  - `references/imagery.md`: the imagery kind that fits each style, treatment rules (crop to the subject with a fixed box, edges per style, no tint through `--ui-accent` while signal colour is on, no text over an image outside a solid panel, an alt decision per image) and a ban list (stock handshake, floating UI cards, abstract blobs, AI-generated faces presented as real people, decorative images with no alt decision). The product-fit table gains an imagery note per row.
  - Control labels use the body face, declared on every button and input with a `1rem` size, since form controls don't inherit the page font: the generic recipe in `SKILL.md`, every catalog control and the demo (`pixel-art` is the stated exception). The generic recipe reads the `--ui-space-*` steps with its old values as fallbacks. `RELEASING.md` gains a pairing-parity step that also searches `examples/`.
  - Workflow step 6, a checklist line and eval 8 (a photographer's portfolio) point to both files.
- **v1.5.0**
  - `references/anti-slop.md`: named tells of a default AI-generated page as a frozen rubric (v1.4). Each of the 21 rows has an id, a severity (high or medium), why it reads as generic, the fix in this skill's vocabulary (tokens, styles, composition moves, guardrails), the condition under which it is not a tell, the evidence that must be visible in source or render, and a counting unit (pattern tells once per page, element tells once per occurrence or per unsupported attribution). The rubric names the inputs its predicates need (source, verbatim brief with content pack, render) marks brief-dependent rows unassessable when the brief is missing, lets a kept aesthetic choice be recorded as retained on an existing-system or user-constraint ground (listed, not counted, never restyled silently; factual rows never), lists the evidence accepted for exceptions in one place, and gives each page a gate result of pass, fail or inconclusive with its assessed coverage. It ends with a five-question "Could this be any site?" test and checks. The tells are prevalence observations from published analyses of AI-built landing pages, not detection methods, and the file says so. Workflow step 5, a checklist line and eval 7 point to it.
- **v1.4.0**
  - `references/composition.md`: three layout moves that work under any style. **Depth planes** (oversized decorative type behind the subject, controls on top), **signal colour** (`--ui-accent` only on interactive elements and their states) and **scale contrast** (one huge element, small supporting text, no middle sizes). Each has a when-to-use table, scoped CSS and checks. Workflow step 4 and a checklist line point to it. Adapted from a short creator tip and bounded by the existing contrast, focus, motion and scoping contracts. Eval 6 covers it.
  - Guardrails borrowed from Textura's public-domain [`next16-claude-starter`](https://github.com/textura-agency/next16-claude-starter) (lessons it records from production sites), rewritten framework-free: first-screen text reveals at full opacity instead of fading from transparent, JavaScript loops that stop under reduced motion, hover-only effects gated to fine pointers, and a new **Phones and overlays** section (`100dvh` plus the safe-area inset, overlays outside transformed ancestors, own overlay colours checked in dark mode, `nowrap` word spans for letter effects, slider `touch-action`, no horizontal overflow at 320 to 430px). The depth-plane back word now clips sideways only, at a line height of 1.1, so letters aren't shaved.
- **v1.3.0**
  - `references/contrast-check.md`: a copy-paste function that computes a pair by the ledger's method, compositing a translucent foreground first, and prints both luminances beside the ratio. It reproduces the ledger's worked example (`D-glass-card-text`, 7.95:1). Added after a live audit where a hand-computed ratio came out 9.15:1 against a true 9.16:1. The rules and the ledger are unchanged.
- **v1.2.2**
  - A ratio you compute must show both luminances, or it isn't called "recomputed". Before claiming "no remote fonts" or "dependencies: none", search every delivered file for `http(s)://`. The scoping rule now covers the inline `<style>` of a demo page. Found by a third blind comparison, where one reply misquoted a border ratio and another claimed no remote fonts while loading Google Fonts.
- **v1.2.1**
  - Healthcare product-fit row now suggests `swiss` as the secondary style, not `bento-grid`. Advisory requests (pick, recommend, explain) get a recommendation without CSS files. The checklist adds a heading-order line and a rule for badge and tag colours. Found by a blind head-to-head comparison against another design skill.
  - Adds a Scoping guardrail (no bare `html`, `body`, `*` or element selectors in drop-in work), a rule that a ledger ratio applies only to the surface it names, a rule that every `<button>` has an explicit `type`, and a rule that "rendered" is claimed only after a real render. Found by a second blind comparison, run against the combined skill set.
- **v1.2.0**
  - `SKILL.md` is now a short routing file. The token blocks moved to `references/tokens-*.md`, and the guardrail CSS and Tailwind mappings moved to their own references.
  - Added a style index, a product-fit table, a "no verified match" contract, a pre-delivery checklist and a contrast ledger that includes derived component pairs.
  - Added related-resources (links and usage rules for components, icons, fonts, motion, charts and companion skills) with a source scorecard, `evals/` and `RELEASING.md`. The description no longer carries hard-coded counts, and names the neighbouring skills it should not replace.
  - The trigger evals were reviewed by hand. They were **not** run through the automated tester.
- **v1.1.0**
  - Token contract with verified contrast.
  - Fixed the Cyberpunk focus and glow clipping and the Pixel Art font declaration.
  - Added Tailwind v4/v3 mappings, guardrails, consistent open-licensed fonts, the existing-design-system rule and the demo page.
  - Corrected the catalog scope claim.
- **v1.0.0**: Initial release.

## License

MIT License © 2026 [JohnSina86](https://github.com/JohnSina86). See [LICENSE](LICENSE).
