# Product fit

Hand-written guidance, **not data**: it records judgement about which styles tend to suit which kinds of product. It was written on 2026-10-01 (imagery notes added 2026-10-13) and has no numeric claims. Treat it as a starting proposal and let the user's brand and audience override it.

## Contents
- [How to use this table](#how-to-use-this-table)
- [Table](#table)
- [No row for the product type](#no-row-for-the-product-type)

## How to use this table
1. Find the closest product type. Propose the **primary** style and the **secondary** style, and give one reason for each, using the *Best for* and *Avoid when* columns of the SKILL.md style index.
2. Never propose a style listed under **Avoid**. If the user asks for one anyway, use it and mention the risk from the index.
3. The style columns hold only style IDs from the SKILL.md index. The last two columns are free text; the imagery note is the starting kind and the first thing to avoid, and [imagery.md](imagery.md) has the full rule set per style.

## Table
| Product type | Primary | Secondary | Avoid | Anti-pattern notes (free text) | Imagery note (free text) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| SaaS product or dashboard | `bento-grid` | `minimalism` | `maximalism`, `pixel-art` | Decoration behind data; low-contrast chart labels. | Cropped screenshots of the real screen; no floating-UI-card hero. |
| Developer tool or CLI landing page | `cybercore` | `minimalism` | `scrapbook`, `victorian` | Paragraphs set entirely in monospace. | A terminal capture or typographic hero; no illustration of a laptop. |
| Fintech or banking | `swiss` | `minimalism` | `maximalism`, `synthwave`, `cyberpunk` | Neon or playful gradients erode trust. | The card or the app, or none; no handshake, no coin clipart. |
| Crypto or web3 dashboard | `cyberpunk` | `glassmorphism` | `scrapbook` | Glow on small numbers; unreadable glass over charts. | 3D or typographic; no rocket or coin clipart. |
| Healthcare or clinic | `minimalism` | `swiss` | `maximalism`, `cyberpunk` | Alarming colour use; small low-contrast text; card-grid layouts for sequential flows such as refills, intake or dosage. | Real people with consent, or none; no AI faces, no stock stethoscope. |
| Wellness or meditation | `ethereal` | `wabi-sabi` | `maximalism`, `cyberpunk` | Auto-playing motion; thin type below weight 400. | Soft-light photo or none; no stock lotus. |
| Luxury or jewellery | `luxury` | `editorial` | `maximalism`, `y2k` | Gold on cream as text; cramped tracking on long lines. | One product shot on cream or dark; no lifestyle collage. |
| Fashion or editorial storytelling | `editorial` | `surrealism` | `pixel-art` | Text over busy imagery without a solid panel. | Reportage photo, full bleed, with a caption in the meta step. |
| Children's education | `claymorphism` | `y2k` | `cybercore`, `victorian` | Dense text blocks; tiny touch targets. | 3D or illustrated characters; no stock classroom. |
| Gaming or esports | `cyberpunk` | `synthwave` | `wabi-sabi` | Long reading in yellow on black. | 3D renders or in-game captures; no stock gamer in a headset. |
| Retro gaming or indie dev hub | `pixel-art` | `synthwave` | `glassmorphism` | Paragraphs in a pixel font. | Pixel sprites at integer scale; no smoothed upscales. |
| Music or streaming | `synthwave` | `glassmorphism` | `swiss` | Glow that blurs small metadata. | Album art and live photos; no abstract waveform blobs. |
| Designer or developer portfolio | `neo-brutalism` | `swiss` | `victorian` | Heavy shadows on every element, which flattens hierarchy. | The work itself, cropped large; no stock desk setup. |
| Architecture or design studio | `swiss` | `wabi-sabi` | `y2k` | Uppercase body copy. | Project photos on the grid, black-and-white allowed; no renders passed off as photos. |
| Restaurant, cafe or artisan shop | `bohemian` | `wabi-sabi` | `cyberpunk` | Decor colours (mustard, terracotta) used for text. | Daylight photos of the food and the room; no stock latte art. |
| Heritage brand, archive or distillery | `victorian` | `editorial` | `neo-brutalism` | Ornament that costs space on mobile. | Engravings and archive photos in a frame; no AI-aged portraits. |
| Smart-home or hardware controls | `neumorphism` | `glassmorphism` | `maximalism` | Raised and pressed states that differ only in shadow. | The device, or none; no stock living room. |
| Festival, event or campaign drop | `maximalism` | `scrapbook` | `neumorphism` | Patterns directly behind text. | Dense illustration or layered cut-outs; no gradient blobs. |
| General e-commerce | `minimalism` | `bento-grid` | `surrealism` | Hidden affordances; icon-only buttons. Use `bento-grid` for homepage highlights only, never for checkout. | Product on a plain background with one consistent crop; no AI-generated model faces. |
| Prototyping or planning tool | `sketch` | `scrapbook` | `luxury` | Hand-drawn look on a payment step. | Line illustration or the tool's own sketches; no polished mockup render. |
| Streetwear or youth brand | `y2k` | `neo-brutalism` | `swiss` | Gloss gradients behind small text. | 3D chrome objects or lookbook photos; no stock model. |
| News or long-form reading | `editorial` | `minimalism` | `maximalism` | Multi-column text on narrow screens. | One photo per story with a caption; no decorative blobs between paragraphs. |

## No row for the product type
- If the request **names or clearly fits an indexed style**, proceed with that style normally and say only that this table has **no product-specific guidance** for the product type.
- If the request fits **no indexed style**, say there is **no verified match**, offer the two closest styles, and label them *unverified*. Do not present them as catalog guidance.
