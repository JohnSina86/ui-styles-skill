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
- **A style index** in `SKILL.md` with aliases, *Best for*, *Avoid when*, a risk flag and the one rule that keeps each style usable, plus a hand-written [product-fit table](references/product-fit.md).
- **A contrast ledger** ([`references/contrast-ledger.md`](references/contrast-ledger.md)) with every role pair and every derived component pair, the method, and a freshness rule.
- **Related resources** ([`references/related-resources.md`](references/related-resources.md)): links, not bundled code, for components, icons, fonts, motion, charts and companion agent skills, chosen by a scored comparison ([`references/source-scorecard.md`](references/source-scorecard.md)), plus rules for using them (licence check, no invented URLs, no run-time remote rules, one icon family per project, tokens and reduced motion still apply). The scores are reported, not independently verified.
- **Evals** in [`evals/`](evals/): four functional tasks and twenty trigger queries (half are near-miss negatives).
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

> **Current release: `v1.2.2`.** To confirm an install, run `git -C <install dir> describe --tags`, which should print `v1.2.2`.

### Claude Code
User level, so the skill is available in every project:
```bash
mkdir -p ~/.claude/skills && git clone --branch v1.2.2 https://github.com/JohnSina86/ui-styles-skill.git ~/.claude/skills/ui-styles
```
```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null; git clone --branch v1.2.2 https://github.com/JohnSina86/ui-styles-skill.git "$HOME\.claude\skills\ui-styles"
```
For project level, run this from the project root:
```bash
mkdir -p .claude/skills && git clone --branch v1.2.2 https://github.com/JohnSina86/ui-styles-skill.git .claude/skills/ui-styles
```
```powershell
New-Item -ItemType Directory -Force ".claude\skills" | Out-Null; git clone --branch v1.2.2 https://github.com/JohnSina86/ui-styles-skill.git ".claude\skills\ui-styles"
```
The folder name must be `ui-styles`, which is the skill's `name`. Claude Code loads the skill on demand from its description, so you don't need to edit a system prompt.

### Google Antigravity
```bash
mkdir -p .agents/skills && git clone --branch v1.2.2 https://github.com/JohnSina86/ui-styles-skill.git .agents/skills/ui-styles          # project
mkdir -p ~/.gemini/config/skills && git clone --branch v1.2.2 https://github.com/JohnSina86/ui-styles-skill.git ~/.gemini/config/skills/ui-styles   # global
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
