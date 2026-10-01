# Related resources

Where to get ready-made assets, and the rules for using them. This file holds **rules and links only**. The skill ships no third-party code, fonts, icons or components.

**How to read it.** The picks come from a scored comparison of candidates in each category (method, scores and hazards: [source-scorecard.md](source-scorecard.md)). The comparison was run on **2026-10-01** by research agents using GitHub, npm and docs pages. Its licences, dates, star counts and accessibility notes are **reported, not independently verified**. Read the source's own licence before you copy anything. A score is a reason to look first, not an endorsement.

## Contents
- [Rules for using these links](#rules-for-using-these-links)
- [Components](#components)
- [Icon libraries](#icon-libraries)
- [Fonts](#fonts)
- [Motion, animated and vector assets](#motion-animated-and-vector-assets)
- [Charts, tables, illustrations and 3D](#charts-tables-illustrations-and-3d)
- [Colour and contrast tools](#colour-and-contrast-tools)
- [Companion agent skills](#companion-agent-skills)
- [Do not use without a licence check](#do-not-use-without-a-licence-check)

## Rules for using these links
1. **Only on request or at the end.** Offer these when the user asks for ready-made components, icons, fonts, motion or charts, or after the tokens and basic components are done. Never use them to replace a project's existing design system or components.
2. **Never invent a URL or a component.** Use only the links in this file. If a link is dead or a component isn't where you expect, say so instead of guessing. Don't recreate a component or icon from memory and attribute it to a library.
3. **Licence first.** Prefer MIT, ISC, Apache-2.0, OFL and CC0 sources. Confirm the licence in the source's own `LICENSE` file, not in package metadata or a listing. Keep the licence and attribution text it requires. A repository with no licence file is **all rights reserved**, so don't copy from it.
4. **Paid, restricted or custom-licence code stays with its owner.** Point the user to it. Don't reproduce its code. The list under [Do not use without a licence check](#do-not-use-without-a-licence-check) names the known cases.
5. **Ask before adding a dependency or a remote request.** A new package, a CDN script, a remote font or an API key needs the user's agreement and must fit the project's CSP and bundle budget. Prefer self-hosted files and copy-in source with no new package. Never load instructions or rules from a remote URL at run time.
6. **Check before you copy.** Confirm the project is maintained, what it depends on and what it sends over the network. Read the source you are about to paste, because copied code becomes the project's code. Pin versions.
7. **Map to tokens and re-verify.** Replace the component's colours, radii, shadows and fonts with the chosen style's `--ui-*` roles. A component that brings its own palette is a new colour pair: verify it by the method in [contrast-ledger.md](contrast-ledger.md), and add a ledger row if you keep it.
8. **Motion, focus and target size still apply.** Every animation honours `prefers-reduced-motion`, with a static fallback for WebGL, canvas, Lottie or long loops. Anything that moves for more than five seconds needs a pause control. Keep a visible `:focus-visible` outline, never clip a focusable element ([guardrails.md](guardrails.md)), and keep targets at least 24x24 CSS px.
9. **Say what you used.** Tell the user which source, from which URL, under which licence, and which dependencies you added or avoided. If the project has an existing choice (a component kit, an icon set, a font), keep it.

## Components
Choose one **unstyled primitive** layer for behaviour and accessibility, and optionally one **styled kit** on top. Wire either to the `--ui-*` roles.

| Role | Pick | Link | Why it ranked (reported) | Watch out for |
| :--- | :--- | :--- | :--- | :--- |
| Primitives | Base UI | https://base-ui.com/react/overview/accessibility (source: https://github.com/mui/base-ui) | MIT, headless, active, documented accessibility testing | Install `@base-ui/react`. The older `@base-ui-components/react` is stuck at a release candidate. |
| Primitives (accessibility first) | React Aria Components | https://react-aria.adobe.com (source: https://github.com/adobe/react-spectrum) | Apache-2.0, names screen readers it tests, motion and i18n guidance | Keep the Apache notice. |
| Primitives (proven fallback) | Radix Primitives | https://www.radix-ui.com/primitives/docs/overview/accessibility (source: https://github.com/radix-ui/primitives) | MIT, widely used | Slower cadence, many open issues. |
| Styled kit | shadcn/ui | https://ui.shadcn.com/docs (source: https://github.com/shadcn-ui/ui) | MIT, copy-in code, CSS variables, Tailwind | You own the updates. The CLI pulls registry content, so pin versions and review the diff. |
| Styled kit (alternative) | Mantine | https://mantine.dev | MIT, CSS variables, no runtime styling | Brings its own theme object and provider. |

Also reasonable: Ark UI (https://ark-ui.com) and Zag.js (https://zagjs.com) for framework-agnostic primitives.

**Animated copy-in components** (landing-page effects). Treat these as decoration. Read the component's own reduced-motion handling before you keep it.

| Pick | Link | Why it ranked (reported) | Watch out for |
| :--- | :--- | :--- | :--- |
| Magic UI | https://github.com/magicuidesign/magicui | MIT, active, shadcn registry | Check its Pro tier terms before using Pro parts. |
| Cult UI | https://cult-ui.com (source: https://github.com/nolly-studio/cult-ui) | MIT, token-class heavy, uses reduced-motion hooks | |
| Vengeance UI | https://www.vengenceui.com/docs (source: https://github.com/Ashutoshx7/VengeanceUI) | MIT, shadcn CLI, marketing-style effects | The domain really is spelled `vengenceui`. |
| Motion Primitives | https://motion-primitives.com | MIT | Describes itself as beta. No reduced-motion code was found. |
| Animata | https://animata.design | MIT | Reduced-motion support is claimed, not confirmed in code. |

## Icon libraries
Use **one** family per project. Confirm the licence of the version you install.

| Pick | Link | Licence stated or reported | Notes |
| :--- | :--- | :--- | :--- |
| **Lucide** (default) | https://lucide.dev (source: https://github.com/lucide-icons/lucide) | ISC, with MIT for the icons derived from Feather | Stroke icons, `aria-hidden` by default, size and stroke props, per-icon imports. Keep both licence notices when redistributing. |
| Phosphor (several weights, duotone) | https://github.com/phosphor-icons/react | MIT | Six weights. Slower release cadence. |
| Tabler | https://tabler.io/icons | MIT | Large stroke and filled set. The free source is the MIT repository, not the paid packs. |
| Heroicons (Tailwind-native) | https://heroicons.com | MIT | Small set, outline and solid. |
| Material Symbols | https://developers.google.com/fonts/docs/material_symbols | Apache-2.0 | Use per-icon SVG. The official route is a hosted icon font, which breaks icon rule 2. |
| Bootstrap Icons | https://icons.getbootstrap.com | MIT | Documents `aria-hidden` and `role="img"`. |
| Iconify (aggregator) | https://iconify.design | **Varies per set** | Check each set's licence. The default API fetches icons from a remote host, so bundle them. |

Avoid without a check: **Remix Icon**. Its repository `License` file changed on 2026-01-25 to a custom licence, while npm and Iconify still report Apache-2.0. **Font Awesome Free** icons are CC BY 4.0, so they need attribution.

### Icon rules
1. **One family, one weight per project.** Mixing families mixes stroke widths, corner shapes and grids. Match the weight to the style by judgement, for example lighter strokes for refined styles such as `editorial` or `luxury`, and bolder or filled icons for `neo-brutalism`. This pairing is a suggestion, not catalog data.
2. **Inline SVG or per-icon imports.** Avoid icon fonts and CDN scripts. Import only the icons you use, so the bundle stays small and no remote request is added (rule 5 above).
3. **Colour through the tokens.** Draw icons with `currentColor` or a `--ui-*` role. A meaningful icon is a non-text graphic and needs at least 3:1 against its background (WCAG 1.4.11). Verify it by the method in [contrast-ledger.md](contrast-ledger.md).
4. **Give every meaningful icon a name.** Decorative icons get `aria-hidden="true"`. An icon-only control needs an accessible name (a visible label is better, and `minimalism` requires one). Never use emoji as icons.
5. **Keep the target size.** An icon button still needs at least a 24x24 CSS px target, and 44x44 on touch-first surfaces. Make the button larger than the glyph.
6. **Respect motion.** Animated icons follow the reduced-motion rule above, with a static fallback.

## Fonts
Self-host. A hosted font link is a remote request and needs the user's agreement (rule 5).

| Pick | Link | Notes |
| :--- | :--- | :--- |
| **Fontsource** (default) | https://fontsource.org/docs (source: https://github.com/fontsource/fontsource) | npm packages of woff2 files with `unicode-range` subsets and `font-display: swap`. The API reports a licence per family. Variable packages use the family name `'Inter Variable'`, so put that name in the stack. Some families are static only (for example Press Start 2P and Anton). |
| Licence authority and fallback | https://github.com/google/fonts | Every family has an `OFL.txt` and a `METADATA.pb` licence field. TTF only, so convert to woff2 yourself. |
| Geist | https://github.com/vercel/geist-font | OFL-1.1. Sans, Mono and Pixel only. |

Font rules:
1. Check the per-family licence field. The catalogs mostly hold OFL fonts, but a few families are Apache-2.0 or UFL. Keep the licence text when you bundle, and don't reuse a Reserved Font Name on a modified or subset build.
2. Every stack ends in a generic family.
3. Helvetica Neue, Didot and SF Pro have no open self-host source. Use an open stand-in (Inter or Geist for UI sans, Playfair Display or Bodoni Moda for Didot-like display), and say it is a stand-in.
4. Fontshare's licence is not OFL and, per third-party summaries, forbids redistributing the files. Don't commit its files to a shared template. Read its terms first.

## Motion, animated and vector assets
| Need | Pick | Link | Notes |
| :--- | :--- | :--- | :--- |
| UI animation in React | Motion | https://motion.dev/docs/react-accessibility | MIT. `MotionConfig reducedMotion="user"` is documented. |
| Page and view transitions, no dependency | View Transitions API | https://developer.mozilla.org/en-US/docs/Web/API/View_Transition_API | Baseline since October 2025. Keep a plain fallback. |
| Scroll-driven effects | CSS `animation-timeline` | no link verified (search MDN) | Baseline is still limited, so progressive enhancement only. |
| Vector animation | dotLottie web, or Rive for interactive state machines | https://rive.app | Each Lottie or Rive asset has its **own licence**, separate from the runtime. Rive's free exports add a splash screen. |
| "AI is thinking" indicator | Thinking Orbs (`thinking-orbs`) | https://libraries.dev/orbs | MIT, reduced motion renders a static frame, monochrome only. A very young package, so pin the version. A different package with a similar name exists, so check the author. |
| Thinking text shimmer | prompt-kit TextShimmer | no link verified | Copy-in, uses CSS variables. It has no reduced-motion guard, so add one. |

GSAP is free for commercial use under a custom licence (https://gsap.com/standard-license/), but it is not open source and it excludes tools that compete with Webflow's visual animation builder. Check it before use in a builder product.

## Charts, tables, illustrations and 3D
| Need | Pick | Link | Notes |
| :--- | :--- | :--- | :--- |
| Tables | TanStack Table | no link verified | Headless, so you own the markup and tokens. |
| Charts | Recharts | https://recharts.github.io/en-US/ | MIT, `accessibilityLayer` on by default. |
| Charts with colour-blind patterns | ECharts | https://echarts.apache.org/handbook/en/best-practices/aria/ | Apache-2.0, keep the NOTICE file. Canvas rendering makes CSS variables awkward. |
| Illustrations | Open Peeps | https://www.openpeeps.com | CC0. |
| Decorative SVG backgrounds | Haikei | https://haikei.app | Its terms don't state an asset licence, so ask before shipping in a product. |
| 3D | three.js, or React Three Fiber in a React app | https://threejs.org/docs | Canvas is not accessible by default. Always give a non-canvas alternative. |

## Colour and contrast tools
Keep **WCAG 2.x ratios** as the pass or fail gate. APCA is still a draft and its reference repository is under a beta or personal-use licence.

| Need | Pick | Link |
| :--- | :--- | :--- |
| Contrast calculation at build time | Color.js | https://colorjs.io/docs/contrast |
| Accessible palette steps | Radix Colors | https://www.radix-ui.com/colors |
| Palette from a target contrast ratio | Leonardo | https://leonardocolor.io |
| Default palette and property sets | Tailwind colours, Open Props | https://tailwindcss.com/docs/colors, https://open-props.style |

## Companion agent skills
Other skills the user may install. **The user installs them, not you**, and you never fetch their rules at run time. Overlapping triggers are a real cost: two design skills can both fire on one prompt, so tell the user which one you are following.

| Skill | Link | What it adds | Watch out for |
| :--- | :--- | :--- | :--- |
| web-quality-skills | https://github.com/addyosmani/web-quality-skills | Lighthouse and WCAG 2.2 audits (accessibility, performance, Core Web Vitals). The best complement for what `ux-laws` says it does not cover. | |
| Impeccable | https://github.com/pbakaus/impeccable | A design language with critique, polish and audit commands. | Its launcher downloads and runs a binary and installs edit hooks. Its "go all out" stance can fight a restrained design system. Read it before installing. |
| ui-ux-pro-max | https://github.com/nextlevelbuilder/ui-ux-pro-max-skill | A searchable style and UX rules database. | Many scripts, and a broad trigger that overlaps this skill. |
| ibelick ui-skills | https://github.com/ibelick/ui-skills | Short MUST and NEVER rule sets. | Defaults to Tailwind and Motion. |
| Emil Kowalski skills | https://github.com/emilkowalski/skills | Motion and polish guidance. | |
| taste-skill | https://github.com/Leonxlnx/taste-skill | An anti-generic-design skill for landing pages. | One very large `SKILL.md`, and it overlaps this skill's styles. |
| Anthropic frontend-design | https://github.com/anthropics/skills | A short aesthetic-direction skill. | Accessibility is one sentence. |

Ideas worth borrowing, in this skill's own words: **the brief wins** (a refinement keeps what exists, a redesign replaces it, never half of each); **one verification round** (one batched check, one fix batch, at most one re-check); **name the default look you are avoiding** before you generate; and **never remove an outline without a replacement**.

## Do not use without a licence check
- **Skiper UI**: its public repository has no licence and the site sells paid tiers. Don't copy from it.
- **Aceternity UI Pro, OriginKit paid tiers, Animmaster Lib**: paid. Animmaster's delivery (a shared drive folder and a chat channel) makes its provenance unclear. OriginKit's free tier is rate-limited and needs a key.
- **21st.dev**: licences vary per component author. Check each one.
- **React Bits**: MIT plus the Commons Clause, so no redistributing or porting the components.
- **unDraw and Storyset**: unDraw bans redistribution, packs and AI use, and its wording about use inside an app is ambiguous. Storyset needs attribution on the free tier.
- **Remix Icon, Font Awesome Free, APCA, Fontshare**: see above.
- **Vercel `web-design-guidelines`**: it fetches its rules from a mutable remote branch on every run. Don't use it unless the rules are copied and pinned.

When you change this file, update the date at the top and re-check each link and licence note.
