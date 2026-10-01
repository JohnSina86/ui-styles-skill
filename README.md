# UI Styles & Visual Themes AI Skill (`ui-styles`)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skill: Antigravity](https://img.shields.io/badge/Skill-Antigravity%20%2F%20Agents-purple.svg)](SKILL.md)

An agentic AI skill providing design tokens, CSS recipes, Tailwind classes, and implementation rules for **22 distinctive UI design styles and visual themes**.

Designed for AI coding assistants (Google Antigravity, Claude Code, Cursor, Copilot) to generate high-fidelity, stylistically coherent user interfaces rather than generic gray-box templates.

---

## The 22 UI Styles at a Glance

| Archetype | Styles Included | Ideal Product Categories |
| :--- | :--- | :--- |
| **1. Dimensional & Tactile** | Claymorphism, Neumorphism, Glassmorphism | Games, Modern OS / Control centers, Smart Home |
| **2. Graphic & Modernist** | Neo-Brutalism, Swiss Design, Minimalism, Maximalism, Editorial Design, Bento Grid | Modern SaaS, Dev tools, Dashboards, Journalism, Design portfolios |
| **3. Retro & Nostalgic** | Y2K Aesthetic, Pixel Art, Synthwave, Victorian | Gaming, Retro culture, Indie music, Heritage brands |
| **4. High-Tech & Futuristic** | Cybercore, Cyberpunk | Terminal interfaces, Web3/crypto, Esports, Hardware telemetry |
| **5. Artistic & Organic** | Scrapbook, Surrealism, Conceptual Sketch, Bohemian, Ethereal, Luxury Typography, Wabi-Sabi | Lifestyle, Fashion, Mindful wellness, Architecture, Fine arts |

---

## Complete Style Directory

| # | Style | Key Aesthetic Feature | Signature Tokens |
|---|---|---|---|
| 1 | **Claymorphism** | 3D puffy, inflated clay shapes | Pastel tones, 4-layer inner/outer shadows, `rounded-3xl` |
| 2 | **Cybercore** | Technical wireframes, HUD overlays | Monospace fonts, thin cyan borders, coordinate grids |
| 3 | **Neo-Brutalism** | Raw, punchy, high-contrast | Thick black borders (`3px`), solid offset shadows (`5px 5px 0 #000`) |
| 4 | **Scrapbook** | Tactile collage, paper textures | Tilted elements (`-2deg`), tape decals, warm cream paper |
| 5 | **Surrealism** | Dreamlike, impossible scale | Radial atmospheric lighting, deep shadows, floating depth |
| 6 | **Y2K Aesthetic** | Late 90s/early 2000s cyber-optimism | Chrome sheen, glossy candy buttons, bubblegum & cyan gradients |
| 7 | **Pixel Art** | 8-bit / 16-bit retro arcade | Stepped block shadows, bitmap fonts (`Press Start 2P`), no antialiasing |
| 8 | **Synthwave** | 1980s neon retrowave | Magenta/cyan dual glows, dark purple backdrops, horizon grids |
| 9 | **Glassmorphism** | Translucent frosted glass | `backdrop-blur-md`, subtle 1px white border (`rgba(255,255,255,0.2)`) |
| 10 | **Neumorphism** | Soft extruded plastic UI | Monochromatic surfaces, dual soft light & dark drop shadows |
| 11 | **Bento Grid** | Modular asymmetric card grid | Rounded containers (`20px–24px`), compact metrics, multi-span cells |
| 12 | **Editorial Design** | High-end print magazine | Display serifs (Playfair/Newsreader), multi-column text, drop caps |
| 13 | **Swiss Design** | Mathematical grid rigor | Bold grotesque sans (Helvetica), Swiss Red accents, strict hierarchy |
| 14 | **Minimalism** | Radical reduction of clutter | Generous negative space, monochrome palette, subtle borders |
| 15 | **Maximalism** | Kinetic visual abundance | Clashing saturated palettes, dense patterns, layered kinetic type |
| 16 | **Luxury Typography** | Understated high fashion | High-contrast serifs (Didone/Bodoni), wide letter tracking, gold accents |
| 17 | **Conceptual Sketch** | Blueprint / hand-drawn napkin | Graph paper grid, irregular borders (`255px 15px...`), pencil ink |
| 18 | **Ethereal** | Ambient mystical glow | Soft pastel blur gradients, translucent layers, delicate type |
| 19 | **Bohemian (Boho)** | Earthy artisanal warmth | Terracotta, olive sage, warm sand, organic curved containers |
| 20 | **Victorian** | 19th-century ornate elegance | Filigree borders, aged parchment, dark burgundy velvet tones |
| 21 | **Cyberpunk** | High-contrast dystopian tech | Neon yellow/cyan on carbon black, angular cut-corners (`clip-path`) |
| 22 | **Wabi-Sabi** | Impermanence & raw texture | Unbleached linen, sumi charcoal ink, quiet asymmetrical balance |

*For complete CSS and Tailwind component recipes, see [`references/styles-catalog.md`](references/styles-catalog.md).*

---

## Installation & Setup

### 1. In Google Antigravity

#### Workspace / Project Level
```bash
# In your project root:
mkdir -p .agents/skills
git clone https://github.com/JohnSina86/ui-styles-skill.git .agents/skills/ui-styles
```

#### Global Level (Machine-Wide)
```bash
# Windows PowerShell
git clone https://github.com/JohnSina86/ui-styles-skill.git "$HOME\.gemini\config\skills\ui-styles"

# macOS / Linux
git clone https://github.com/JohnSina86/ui-styles-skill.git ~/.gemini/config/skills/ui-styles
```

### 2. In Other Agentic AI Assistants (Claude Code, Cursor, Copilot)
Add a reference in your system prompt or `.cursorrules`:
```markdown
When designing or building UI components, consult the UI Styles Skill in .agents/skills/ui-styles/SKILL.md to adhere to the designated theme and CSS tokens.
```

---

## Example Prompts

* *"Build a hero section and pricing card in Neo-Brutalism style using Tailwind CSS."*
* *"Restyle our dashboard using Bento Grid architecture and subtle Glassmorphism."*
* *"Create an artisan coffee homepage adhering to the Bohemian and Wabi-Sabi aesthetic."*
* *"Generate a cyberpunk HUD status widget with angular cut corners."*

---

## License

MIT License © 2026 [JohnSina86](https://github.com/JohnSina86). See [LICENSE](LICENSE) for details.
