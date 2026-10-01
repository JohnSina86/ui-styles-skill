# Related resources

A short list of third-party sources for **ready-made animated components**, and the rules for using them. These are **pointers, not endorsements**: this skill has not reviewed their code, licences or accessibility. Links and descriptions were gathered from search results on **2026-10-01**, and only one site was opened. Treat every description as unverified until you read the source.

## Contents
- [Links](#links)
- [Rules for using these links](#rules-for-using-these-links)

## Links
| Name | Link | What it is, as described by third parties | Delivery | Licence note (unverified) |
| :--- | :--- | :--- | :--- | :--- |
| OriginKit | https://originkit.dev | Free animated component library for websites | Copy code, Framer, or MCP | Check the site's terms |
| Skiper UI | https://skiper-ui.com (source: https://github.com/nischayhq/skiper-ui) | Animated "un-common" components for shadcn/ui, built with React, Tailwind and Framer Motion | Copy and paste | Listings say free with attribution on the free tier. Confirm. |
| Vengeance UI | https://www.vengenceui.com/docs (source: https://github.com/Ashutoshx7/VengeanceUI) | Animated React components for landing pages (note the domain spelling) | CLI that copies editable source files into your project | Check the repository licence |
| Animmaster Lib | https://animmasterlib.dev | A paid "PRO" library of animated components using GSAP and WebGL | Purchased access | Paid. Don't reproduce its code. |
| Thinking Orbs | https://orbs.jakubantalik.com (listing: https://21st.dev/@larsen66/components/thinking-orbs) | Animated "AI is thinking" indicators for chat UIs | npm package (`thinking-orbs`) or copy | Check the repository licence |

## Rules for using these links
1. **Only on request or at the end.** Offer these when the user asks for ready-made or animated components, or after the tokens and basic components are done. Never use them to replace a project's existing design system or components.
2. **Never invent a URL or a component.** Use only the links above. If a link is dead or a component isn't where you expect, say so instead of guessing. Don't recreate a component from memory and attribute it to a library.
3. **Check before you copy.** Confirm the licence and any attribution requirement, that the project is maintained, and what dependencies it needs. Read the source you are about to paste, because copied code becomes the project's code.
4. **Paid or restricted code stays with its owner.** For a paid library, point the user to it. Don't reproduce its code.
5. **Ask before adding a dependency or a remote request.** A new package (Framer Motion, GSAP, a WebGL runtime), a CDN script or a remote font needs the user's agreement and must fit the project's CSP and bundle budget. Prefer copy-paste source with no new package.
6. **Map to tokens and re-verify.** Replace the component's colours, radii, shadows and fonts with the chosen style's `--ui-*` roles. A component that brings its own palette is a new colour pair: verify it by the method in [contrast-ledger.md](contrast-ledger.md), and add a ledger row if you keep it.
7. **Motion and focus rules still apply.** Every animation must honour `prefers-reduced-motion`, with a static fallback for WebGL, canvas or long loops. Anything that moves for more than five seconds needs a pause control. Keep a visible `:focus-visible` outline, and never clip a focusable element ([guardrails.md](guardrails.md)).
8. **Report what you used.** Tell the user which component, from which URL, under which licence, and which dependencies you added or avoided.

If you change this list, update the date above, and re-check each link and licence note.
