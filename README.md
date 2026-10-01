# UI Styles & Visual Themes AI Skill (`ui-styles`)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skill: Agents](https://img.shields.io/badge/Skill-Claude%20Code%20%2F%20Antigravity-purple.svg)](SKILL.md)

An agent skill with **contrast-verified design tokens and CSS/Tailwind recipes for 22 distinctive UI styles**. It's designed for AI coding assistants (Claude Code, Google Antigravity, Cursor, Copilot), so they produce coherent, accessible themes instead of generic grey-box templates.

## What's inside

- **One token block per style** with fixed role names (`--ui-bg`, `--ui-surface`, `--ui-text`, `--ui-accent`, `--ui-border`, `--ui-focus`, …), so components never hard-code colours.
- **Every text and control colour pair is computed against WCAG 2.x.** Colours that fail are marked *decorative only*.
- **Tailwind mappings** for v4 (`@theme inline`) and v3 (`theme.extend`).
- **Shared guardrails:** visible focus, `prefers-reduced-motion`, `prefers-reduced-transparency`, a `backdrop-filter` fallback, self-hosted font loading and dark-mode notes.
- **Detailed component recipes** (card, button, input) for 6 styles in [`references/styles-catalog.md`](references/styles-catalog.md). The other 16 are built from their tokens using the shared role pattern.
- **A runnable demo:** [`examples/cyberpunk-glass.html`](examples/cyberpunk-glass.html).

## The 22 styles

| Archetype | Styles |
| :--- | :--- |
| Dimensional & Tactile | Claymorphism, Neumorphism, Glassmorphism |
| Graphic & Modernist | Neo-Brutalism, Swiss Design, Minimalism, Maximalism, Editorial Design, Bento Grid |
| Retro & Nostalgic | Y2K Aesthetic, Pixel Art, Synthwave, Victorian |
| High-Tech & Futuristic | Cybercore, Cyberpunk |
| Artistic & Organic | Scrapbook, Surrealism, Conceptual Sketch, Ethereal, Bohemian, Luxury Typography, Wabi-Sabi |

Each style in [`SKILL.md`](SKILL.md) §4 lists its visual DNA, tokens, decorative-only colours, *Best for* and *Avoid when*. The *Avoid when* lines point to the relevant law in the companion [ux-laws skill](https://github.com/JohnSina86/ux-laws-skill).

## Installation

Install a tagged release, so you get a reviewed version and not whatever the default branch holds later.

### Claude Code
User level, so the skill is available in every project:
```bash
mkdir -p ~/.claude/skills && git clone --branch v1.1.0 https://github.com/JohnSina86/ui-styles-skill.git ~/.claude/skills/ui-styles
```
```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null; git clone --branch v1.1.0 https://github.com/JohnSina86/ui-styles-skill.git "$HOME\.claude\skills\ui-styles"
```
For project level, run the same command from the project root with the target `.claude/skills/ui-styles`. The folder name must be `ui-styles`, which is the skill's `name`. Claude Code loads the skill on demand from its description, so you don't need to edit a system prompt.

### Google Antigravity
```bash
mkdir -p .agents/skills && git clone --branch v1.1.0 https://github.com/JohnSina86/ui-styles-skill.git .agents/skills/ui-styles          # project
mkdir -p ~/.gemini/config/skills && git clone --branch v1.1.0 https://github.com/JohnSina86/ui-styles-skill.git ~/.gemini/config/skills/ui-styles   # global
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

- **v1.1.0**
  - Token contract with verified contrast.
  - Fixed the Cyberpunk focus and glow clipping and the Pixel Art font declaration.
  - Added Tailwind v4/v3 mappings, guardrails, consistent open-licensed fonts, the existing-design-system rule and the demo page.
  - Corrected the catalog scope claim.
- **v1.0.0**: Initial release.

## License

MIT License © 2026 [JohnSina86](https://github.com/JohnSina86). See [LICENSE](LICENSE).
