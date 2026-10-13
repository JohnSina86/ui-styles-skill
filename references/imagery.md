# Imagery direction

Which kind of image fits each style, how to treat it, and what never to use. Imagery is the fastest way for a page to look like every other page, so the decision is made once, named, and checked. It adds no colours: the contrast contract, the style's `Requires` rule, the signal colour move in [composition.md](composition.md) and the guardrails still win.

These are craft heuristics, not graded rules. `ux-laws` grades what the image does to the task, never which kind was chosen.

## Contents
- [1. Kinds](#1-kinds)
- [2. Per style](#2-per-style)
- [3. Treatment](#3-treatment)
- [4. Banned](#4-banned)
- [Checks](#checks)

## 1. Kinds
Name one kind per page (or per view, if the page mixes) before you build. "None" is a decision, not a gap: layout, type and colour carry the page.

| Kind | Means | Needs |
| :--- | :--- | :--- |
| photo | a photograph of the real product, place, work or people | the user's own photos or a licensed source named in the delivery |
| illustration | drawn or painted artwork, flat or textured, in the style's palette | one drawing style across the page |
| 3D | rendered objects, cut out or on the page background | a render the user supplies; the skill doesn't make one |
| typographic | the type is the image: the depth-planes back word, a huge numeral, a wordmark | the scale in [typography.md](typography.md) |
| none | no images; the page is type, colour and layout | the same, plus the composition moves |

## 2. Per style
One row per style ID in the SKILL.md index, in index order. *Fits* is the kind to propose; *Also* is the one alternative that holds; anything else needs a reason.

| ID | Fits | Also | Treatment |
| :--- | :--- | :--- | :--- |
| `claymorphism` | 3D | illustration | Soft clay renders, cut out, on `--ui-surface`, with the card's tinted shadow. No photographs: they puncture the inflated look. |
| `cybercore` | typographic | none | Read-outs, coordinates and 1px wireframe drawings in `--ui-text-muted`. A cropped screenshot of the tool is the only photo-like image. |
| `neo-brutalism` | photo | illustration | Cut-out or hard-cropped, inside a `--ui-border` frame with the offset shadow. The image is a block in the grid, never a backdrop. |
| `scrapbook` | photo | illustration | Polaroid frame and tape are decoration. Rotation up to 3deg on the frame only; captions stay level. |
| `surrealism` | photo | 3D | One subject, cut out, at an unexpected scale, floating on `--ui-bg` in the violet glow. Text never crosses it. |
| `y2k` | 3D | typographic | Chrome, bubbles and glossy objects. Gloss stays on objects; the chrome gradient is decor, never behind text. |
| `pixel-art` | illustration | none | Sprites at integer scale with `image-rendering: pixelated`. No photographs, no smoothed upscales. |
| `synthwave` | illustration | typographic | Horizon grid and sunset as a backdrop. Glow on the drawing, not on text under 24px. No photographs. |
| `glassmorphism` | photo | 3D | The backdrop is the image: full bleed, dark or saturated, so the glass contract holds. Text only inside the glass panel, whose pairs are verified over white, the worst case (ledger rows `D-glass-card-text`, `D-glass-muted`). |
| `neumorphism` | none | illustration | The surface is the image. Monochrome icons in `--ui-text`. A product shot sits only inside a pressed well. |
| `bento-grid` | photo | illustration | Screenshots of the real screen, cropped to the card edge at `--ui-radius`. At most one image per card. |
| `editorial` | photo | illustration | Reportage, at column width or full bleed, each with a caption in the meta step. The hero is one photo, not a grid. |
| `swiss` | photo | typographic | One photo filling exact grid cells, no radius. Black-and-white is allowed. Red stays on type and rules. |
| `minimalism` | photo | none | One large image per view on `--ui-bg`, `object-fit: contain`, no frame, no shadow. |
| `maximalism` | illustration | photo | Dense layering and cut-outs behind solid `--ui-surface` text panels. The pattern is decoration, not content. |
| `luxury` | photo | none | One product or material shot, monochrome, on cream or dark, with space around it. No gold tint: gold is ornament only. |
| `sketch` | illustration | none | Pencil lines in `--ui-text` on the graph paper. A photograph reads as finished work and clashes. |
| `ethereal` | photo | illustration | Soft light, diffuse. The one style where a feathered edge (`mask-image` into `--ui-bg`) is allowed. No hard frames. |
| `bohemian` | illustration | photo | Botanical line or watercolour; photos in daylight of hand-made goods. Terracotta and mustard stay decor, not image tints. |
| `victorian` | illustration | photo | Engravings in `--ui-text` on parchment. A photo sits inside the double-rule frame. |
| `cyberpunk` | 3D | photo | Hard-surface renders or night photography. Cut corners go on a wrapper, never on a focusable element. Scanlines are decoration. |
| `wabi-sabi` | photo | none | Texture close-ups (stone, clay, linen), matte, placed asymmetrically with space. No filter, no frame. |

## 3. Treatment
- **Crop to the subject.** Fix the box with `aspect-ratio` plus `width` and `height` attributes, then `object-fit: cover` with `object-position` toward the subject. A cover crop changes with the box, so check it at 375 and 1440. Never cut a product or a face at the edge of its frame.
- **Edges follow the style.** Hard edge at `--ui-radius` by default. Cut-outs (transparent PNG or WebP) for depth-plane subjects and the styles whose row says so. Frames only where the row names one. Feathered edges only on `ethereal`. No drop shadow on a photo unless the style's `--ui-shadow` applies to its cards.
- **No tint through `--ui-accent` while signal colour is on.** A duotone, overlay, gradient or icon fill in the accent makes decoration look tappable (composition.md, move 2). Greyscale, or a tint in a decorative-only colour, is allowed where the row says so. Otherwise photos keep their own colour: no filter stack.
- **Text over an image needs a verified panel.** A solid `--ui-surface` or plane is verified by its ledger row. A translucent panel is allowed only when its exact text and surface pair has a ledger row computed against the worst-case backdrop, as the glass rows are (`D-glass-card-text` 7.95:1 and `D-glass-muted` 5.35:1 over pure white, in [contrast-ledger.md](contrast-ledger.md)). Any other translucent panel needs the same worst-case recomputation with [contrast-check.md](contrast-check.md), luminances shown. A gradient scrim is not a panel, and a style whose `Requires` rule says solid panels (`surrealism`, `y2k`) gets no translucent exception.
- **Alt decision, per image.** Every `<img>` carries either a descriptive `alt` (the subject, not "image of") or `alt=""` because it is decoration, and the delivery says which. A `background-image` carries no content. An image that is a link's only content gets the destination as its `alt`. A gallery image gets its subject, never the file name.
- **Layout and loading.** `width` and `height` on every image so nothing shifts. `loading="lazy"` below the fold; the hero image loads eagerly. Dark mode: images don't invert, and a cut-out on `--ui-bg` is checked in both modes.
- **Motion.** Parallax or drift on an image is decorative: `data-ui-motion`, static under reduced motion (guardrails, Motion). Video follows the same rule and needs a poster.

## 4. Banned
Never used, whatever the style or product. Each has a reason and a replacement.

| Banned | Why | Instead |
| :--- | :--- | :--- |
| Stock handshake, and its cousins (pointing at a laptop, a team laughing at nothing) | It fits any site, so it says nothing about this one. | The product, the place, the people who make it, or none. |
| Floating UI cards (a hero illustration of cards, charts and toggles hovering in space) | The default SaaS hero: it says "dashboard" without showing yours. | A cropped screenshot of the real screen, or typographic. |
| Generic abstract blobs, gradient orbs and meshes as the subject | Decoration standing in for an image. | Typographic, or none. A gradient orb is allowed only as the `glassmorphism` backdrop, never as the subject. |
| AI-generated faces presented as real people (testimonials, team, customers) | Misrepresentation. A reader who spots it stops trusting the page. | Real people with consent, initials or avatars with no face, or no faces. |
| Decorative images with no alt decision | A screen reader announces the file name, or nothing, at random. | `alt=""` for decoration, a descriptive `alt` for content, decided per image (section 3). |

## Checks
Add these to the section 7 checklist when the page has imagery, or when you chose none.
- [ ] **Kind named:** photo, illustration, 3D, typographic or none, from the style's row or with a reason.
- [ ] **Treatment:** boxes fixed with `aspect-ratio`, crops checked at 375 and 1440 or left open as "needs a render", edges per the row, no tint or overlay in `--ui-accent`, no text over an image outside a panel verified against the worst-case backdrop (solid, or a translucent pair with a worst-case ledger row).
- [ ] **Alt:** every `<img>` has a descriptive `alt` or `alt=""`, and the delivery lists which.
- [ ] **Ban list:** nothing from section 4, and the image source (the user's, or a named licence) is stated.
