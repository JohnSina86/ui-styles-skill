# Reveal choreography

How the first screen arrives. A reveal is a sequence, not a set of effects: things enter in an order, inside a time budget, and most of the screen never moves at all. Use this file only when the page has a first-screen reveal (a loader, a staggered hero, an entrance of any kind). A page with no reveal records `choreography: none` and skips it.

It adds no colours and no roles, and every contract still applies: the Motion, Focus and Phones rules in [guardrails.md](guardrails.md), the Scoping rule, and the ledger. **Source:** rewritten from Textura's public-domain [`next16-claude-starter`](https://github.com/textura-agency/next16-claude-starter) (its animation system, motion rules, motion reviewer, mobile QA notes and fix catalogue, recorded from production sites), without its animation library or framework. Framework-free CSS only.

## Contents
- [The order](#the-order)
- [Timing budget](#timing-budget)
- [What moves and what never does](#what-moves-and-what-never-does)
- [Reduced motion: a static end state](#reduced-motion-a-static-end-state)
- [One choreographed section per view](#one-choreographed-section-per-view)
- [The marker](#the-marker)
- [CSS example](#css-example)
- [Record it](#record-it)
- [Checks](#checks)

## The order
Four steps, in this sequence. Skip a step and the ones after it move up; never reorder them.

1. **Loader, or none.** Default to none. A loader is justified only when the first screen would otherwise show something broken while it loads (a scene, a large hero image, a font the display heading depends on). It is opaque, carries `--ui-bg` and `--ui-text`, and belongs to a page you own, never to a drop-in component. It animates by `transform` or `clip-path`, never by its own box (a bar that grows by `width` shifts layout). It locks the scroll while it is up and the page starts at the top when it leaves: set `history.scrollRestoration = "manual"` while the loader is up, scroll to `0` as it lifts, and put the previous value back when the gate closes. It does not run on a reload, on history navigation (Back, Forward) or on a fragment URL: those keep the browser's own scroll position, so the script returns before setting the gate. A smooth-scroll script ignores `overflow: hidden`, so stop it while the loader is up and check nothing restarts it. The gate waits for what the first screen depends on: the display font (`document.fonts.ready`) and the hero image (`img.decode()`), together, so the subject never animates in as an empty box and pops in after the sequence. The hero image carries `width` and `height` (or an `aspect-ratio`) so its box is reserved from first paint, and it is never `loading="lazy"`. An image that fails to decode resolves the wait like a loaded one; one that is still loading when the deadline fires does not hold the page: the loader goes, the box stays reserved and the image fills it when it arrives. A loader that waits on an asset gets a deadline (about 3 s) armed the moment the gate is set, not when the document finishes parsing; when it fires, the loader is removed and the gate and scroll state released, and a readiness callback that arrives later does nothing. One terminal cleanup runs on every end: the exit, the deadline, a failed wait, `pagehide`, and a change to reduced motion while the loader is up.
2. **The gate.** Choreographed elements hold their start pose while the loader is up, so nobody sees them mid-entrance through the curtain. The gate is an attribute a short inline script in `<head>` sets on the theme element before the body parses, and removes the moment the loader starts to exit, so the first steps play under the clearing curtain. The loader is hidden by default and shown only by the gate, so with script disabled or blocked by the CSP there is no gate and no loader: the reveal plays from first paint and the page is usable. The content is in the HTML at rest; the start pose is only the first keyframe. The loader never holds keyboard focus back: `aria-hidden` hides only the loader, and the controls under it stay focusable, so the moment focus enters the covered content (a `focusin` on the document) the cleanup runs and the loader is gone before any control can be activated unseen.
3. **Staggered content.** Headings and decoration enter first, one step apart: the back-plane word, then each heading line, then an eyebrow or meta line. Each line is its own element (a `span` per line, letters grouped in `white-space: nowrap` word spans if the effect is per letter). Delays are multiples of one `--ui-stagger` step, never hand-picked values.
4. **The hero subject last.** The product cut-out, portrait, illustration or video enters after the type, so the eye lands on it as the sequence settles. It is the last element to come to rest. Controls and body text are not in the sequence: they are at rest from the first frame.

## Timing budget
The clock starts when the gate opens (the loader begins to lift) or, without a loader, at first paint. The 1.2 s budget covers the reveal after the lift; the wait before it is bounded separately by the loader's deadline (about 3 s), and a delivery note reports both numbers.

| Budget | Value |
| :--- | :--- |
| Last first-screen element at rest | under 1.2 s |
| Stagger step (`--ui-stagger`) | 40 to 80 ms |
| Latest start of any first-screen element | 600 ms |
| Entrance duration, type | 400 to 600 ms |
| Entrance duration, subject | 500 to 700 ms |
| Loader exit | 300 to 500 ms, overlapping the first steps |

So the hero in the example below, with a 60 ms step, runs: back word at 0 ms, two heading lines at 60 and 120 ms, eyebrow at 180 ms, then a three-step pause, and the subject at 420 ms for 600 ms, at rest by 1.02 s. If the sum exceeds 1.2 s, remove elements from the sequence; don't shorten the step below 40 ms, which reads as a flicker. First screen means what is visible before scrolling at a phone width (375px) and a desktop width (1440px); check both.

## What moves and what never does
| Choreographed | At rest from the first frame |
| :--- | :--- |
| Headings of the section (display, `h1`, `h2`, eyebrow) | Buttons, links, inputs, the nav, the menu toggle, the skip link |
| Media: image, video, canvas, illustration | Body text, labels, prices, captions, form help, status and error text |
| Decoration: the back-plane word, rules, shapes, badges that do nothing | A cookie or consent banner, alerts, anything `aria-live` |

Controls appear at rest so a visitor can act on the first frame and a hit test gives the same answer at every moment; under a loader, the first keyboard focus dismisses it (The order, step 2). Body text appears at rest so a contrast sample at any moment reads the ledger ratio. Headings on the first screen follow the Motion guardrail on fades ([guardrails.md](guardrails.md), Motion): transform, `clip-path` or a mask at full opacity, and no mask over glass.

Animate `transform` and `clip-path` only. Never `width`, `height`, `top`, `margin` or `font-size` (layout shifts, and the hit area moves). No `filter: blur()` per letter or word; if the style wants blur, one filter per line, removed at rest. Hover effects are not choreography and sit under `(hover: hover) and (pointer: fine)`.

## Reduced motion: a static end state
Under `prefers-reduced-motion: reduce` the page is complete and readable at first paint: every choreographed element sits at its end pose, nothing is clipped, nothing is paused, and there is no loader and no gate. The guardrail block ends every animation after one tick but keeps `animation-delay`, so an element with a 600 ms delay and a backwards fill would sit clipped for 600 ms. The choreography therefore adds its own rule: `animation: none` and `clip-path: none` on every `[data-ui-reveal]` element, and the loader is not shown. The script checks `matchMedia('(prefers-reduced-motion: reduce)')` before it sets the gate and listens for the query to change: if reduction is requested while the loader is up or exiting, the cleanup runs at once (loader removed, gate and scroll state released, pending lift cancelled) instead of waiting for an `animationend` that a cancelled animation never fires. A loader that is also a loop (a spinner, a counter) stops under reduced motion, or it can hang the page (guardrails, Motion).

## One choreographed section per view
One section per view above the fold gets a sequence, and it is almost always the hero. A second sequence in the same view competes with the first and doubles the budget.

Sections below the fold get no choreography. Each may have at most **one inview reveal**: the section's heading or media enters once by transform or `clip-path` when it scrolls into view (an `IntersectionObserver` with a threshold, unobserved after the first entry), never replayed on the way back up, and never on body text or controls. Everything else below the fold is static. A page where every section slides in on scroll is a tell, not a design.

## The marker
Two attributes, with different jobs:
- `data-ui-motion` is the shared reduced-motion marker from [guardrails.md](guardrails.md) (Motion). It also sits on hover and press effects (the Neo-Brutalism press offset, Scrapbook tilts), so it does not identify the sequence.
- `data-ui-reveal` marks membership of the sequence: every choreographed element, the loader and each inview reveal carry it, beside `data-ui-motion`. The gate selector pauses `[data-ui-reveal]`, this file's reduced-motion rule removes its animation and clip, and a reviewer counts it: the number of `data-ui-reveal` attributes in the markup equals the number of elements the delivery line names. A button marked `data-ui-motion` for its press effect is not in that count. An element in the sequence without both attributes is a defect.

## CSS example
Scoped under `.theme-swiss`; replace the id. A short inline script in `<head>` sets the gate before first paint and lifts it; the loader is hidden until the gate shows it. The content is in the HTML at rest, the start pose is a keyframe, and every entrance runs at `opacity: 1`.

```html
<div class="ui-loader" data-ui-reveal data-ui-motion aria-hidden="true"><span>Aura</span></div>
<section class="ui-hero">
  <p class="ui-plane-back ui-enter" style="--ui-i: 0" data-ui-reveal data-ui-motion aria-hidden="true">AURA</p>
  <h1><span class="ui-enter" style="--ui-i: 1" data-ui-reveal data-ui-motion>Sound you can</span><br>
      <span class="ui-enter" style="--ui-i: 2" data-ui-reveal data-ui-motion>see in the room</span></h1>
  <p class="ui-eyebrow ui-enter" style="--ui-i: 3" data-ui-reveal data-ui-motion>Studio headphones</p>
  <img class="ui-subject" style="--ui-i: 7" data-ui-reveal data-ui-motion src="headphones.png" width="1200" height="1200" alt="Aura Studio headphones in sage green">
  <p>Open-back drivers tuned for mixing rooms. Ships in three days.</p>
  <button type="button" class="ui-button">Add to bag</button>
</section>
```
```css
.theme-swiss { --ui-stagger: 60ms; }
/* Gate: held while the theme element carries data-ui-loading. The loader is excluded so its own exit can run. */
.theme-swiss[data-ui-loading] { overflow: hidden; }
.theme-swiss[data-ui-loading] [data-ui-reveal]:not(.ui-loader) { animation-play-state: paused; }
/* Loader: hidden until the gate shows it (no script, no loader); opaque; exits by clip, not by its box. */
.theme-swiss .ui-loader { display: none; position: fixed; inset: 0; z-index: 10; place-items: center; background: var(--ui-bg); color: var(--ui-text); font-family: var(--ui-font-display); }
.theme-swiss[data-ui-loading] .ui-loader, .theme-swiss .ui-loader.is-done { display: grid; }
.theme-swiss .ui-loader.is-done { animation: ui-lift 400ms cubic-bezier(0.76, 0, 0.24, 1) forwards; }
@keyframes ui-lift { to { clip-path: inset(0 0 100% 0); } }
/* Type and decoration: a clip wipe with a short rise, opacity stays 1. */
.theme-swiss .ui-enter { display: inline-block; animation: ui-rise 500ms cubic-bezier(0.22, 1, 0.36, 1) both; animation-delay: calc(var(--ui-i, 0) * var(--ui-stagger)); }
@keyframes ui-rise { from { transform: translateY(0.4em); clip-path: inset(0 0 100% 0); } to { transform: none; clip-path: inset(0); } }
/* Subject: last, after the type. Step 7 = 420 ms start + 600 ms = at rest by 1.02 s. */
.theme-swiss .ui-subject { animation: ui-subject 600ms cubic-bezier(0.22, 1, 0.36, 1) both; animation-delay: calc(var(--ui-i, 0) * var(--ui-stagger)); pointer-events: none; max-width: 100%; height: auto; }
@keyframes ui-subject { from { transform: translateY(24px) scale(0.96); clip-path: inset(100% 0 0 0); } to { transform: none; clip-path: inset(0); } }
/* Reduced motion: no loader, no gate, every element at its end pose at first paint. */
@media (prefers-reduced-motion: reduce) {
  .theme-swiss .ui-loader { display: none !important; }
  .theme-swiss [data-ui-reveal] { animation: none !important; clip-path: none !important; }
}
```
```js
/* Inline in <head>, before the body, so the gate exists before first paint. Without script none of this runs: no gate, no loader, page at rest. */
(() => {
  const motion = matchMedia('(prefers-reduced-motion: reduce)'), nav = performance.getEntriesByType('navigation')[0];
  if (motion.matches || (nav && (nav.type === 'back_forward' || nav.type === 'reload')) || location.hash) return;   /* reduced motion, reload, history or fragment navigation: no loader, the browser keeps its scroll position */
  const root = document.documentElement, previous = history.scrollRestoration;
  let state = 'gated';                                        /* gated -> lifting -> done; done is terminal */
  history.scrollRestoration = 'manual'; root.setAttribute('data-ui-loading', '');
  const release = () => { clearTimeout(deadline); root.removeAttribute('data-ui-loading'); history.scrollRestoration = previous; };
  const done = () => { if (state === 'done') return; state = 'done'; release(); root.querySelector('.ui-loader')?.remove(); };
  const lift = () => {                                        /* the only path that plays the exit; a late or repeated call does nothing */
    if (state !== 'gated') return;
    const loader = root.querySelector('.ui-loader');
    if (!loader) return done();
    state = 'lifting'; window.scrollTo(0, 0); release(); loader.classList.add('is-done');
    loader.addEventListener('animationend', done, { once: true }); setTimeout(done, 500);   /* animationend or the timer, whichever comes first */
  };
  const deadline = setTimeout(done, 3000);                    /* armed now, not at DOMContentLoaded: a stalled script cannot keep the page covered */
  addEventListener('pagehide', done, { once: true });
  addEventListener('focusin', done, { once: true });          /* keyboard focus entered the covered content: dismiss the loader, never activate a control unseen */
  motion.addEventListener('change', e => { if (e.matches) done(); });   /* reduction requested mid-way: end it now */
  addEventListener('DOMContentLoaded', () => {                /* wait for the display font and the hero image together; the deadline bounds both */
    const subject = root.querySelector('.ui-subject');
    const image = subject && subject.decode ? subject.decode().catch(() => {}) : Promise.resolve();   /* a failed image does not block the lift */
    Promise.all([document.fonts.ready, image]).then(lift, lift);
  });
})();
```
The `ui-enter` spans are `inline-block` so `transform` applies; the `h1` keeps its line height at 1.1 or more so the clip never shaves glyphs. If the project's CSP forbids inline styles, set each `--ui-i` in the stylesheet instead. The back word is the depth-planes move from [composition.md](composition.md) and keeps its rules (decorative, `aria-hidden`, clipped sideways only). `pointer-events: none` on the subject is the same move's rule: a transparent image still takes clicks.

## Record it
Write one line in the delivery, matching the SKILL.md workflow step:
- `choreography: hero: loader 400 ms; step 60 ms; back word 0, heading lines 60/120, eyebrow 180, subject 420 for 600 ms; at rest by 1.02 s; 6 data-ui-reveal elements` or
- `choreography: none`.

## Checks
Add these to the section 7 checklist when the page has a reveal.
- [ ] **Order:** loader (or none), gate, staggered type and decoration, subject last. The loader exits by `transform` or `clip-path`, locks the scroll and leaves the page at the top.
- [ ] **Budget:** every first-screen element starts by 600 ms and is at rest under 1.2 s; the step is 40 to 80 ms, taken from `--ui-stagger`. The timings are written in the delivery line.
- [ ] **At rest:** no control, body text, label, price, banner or live region is in the sequence. Nothing animates `width`, `height`, `top`, `margin` or `font-size`.
- [ ] **Opacity:** first-screen headings enter by transform, `clip-path` or mask at full opacity (guardrails, Motion). No mask over glass.
- [ ] **Reduced motion:** with `prefers-reduced-motion` emulated, no loader, no gate, every element at its end pose, the page fully readable at first paint. No loop runs.
- [ ] **One section:** one choreographed section per view above the fold; below it only inview reveals that play once on headings or media.
- [ ] **Marker:** `data-ui-reveal` beside `data-ui-motion` on every choreographed element, the loader and each inview reveal; the `data-ui-reveal` count matches the elements named in the delivery line. Hover and press effects keep `data-ui-motion` alone.
- [ ] **Lifecycle:** the loader is hidden until the gate shows it; the gate waits for the display font and the hero image together, and the image has `width` and `height` (or `aspect-ratio`) so its box is reserved; the deadline is armed when the gate is set; reload, history and fragment navigation skip the loader and the top scroll; one idempotent cleanup releases the gate, restores `history.scrollRestoration` and removes the loader on exit, deadline, failure, `pagehide`, the first keyboard focus and a reduced-motion change, and a late readiness callback cannot restart the exit.
- [ ] **Render:** say "rendered" only if the reveal was watched in a browser tool in this session, at 375px and 1440px; otherwise leave the order, budget and reduced-motion items open and say so. Reading the code proves the rules are written, not that they play.
