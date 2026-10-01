# UI Styles: Component Catalog

This catalog has **detailed component recipes (card, button, input) for 6 of the 22 styles**: Neo-Brutalism, Glassmorphism, Bento Grid, Cyberpunk, Swiss and Wabi-Sabi. Three of them (Neo-Brutalism, Glassmorphism, Bento Grid) also have a Tailwind version. For the other 16 styles, build components from the style's token block in `SKILL.md` §4, using the role pattern in `SKILL.md` §6.

Every recipe reads colours from the `--ui-*` tokens, so add the style's token block (`.theme-<name>`) first. The shared focus, motion, transparency and font rules are in `SKILL.md` §5.

---

## Quick matrix

The fonts here match the token blocks in `SKILL.md`. All of them are open-licensed and on Google Fonts.

| Style | Display / body font | Border | Elevation | Radius |
| :--- | :--- | :--- | :--- | :--- |
| Claymorphism | Nunito | none | tinted outer + inner shadows | 24px |
| Cybercore | JetBrains Mono | 1px cyan | inset cyan glow | 2px |
| Neo-Brutalism | Space Grotesk | 3px black | 5px offset, no blur | 8px |
| Scrapbook | Caveat / Lora | 1px warm grey | soft drop + tilt (decor only) | 3px |
| Surrealism | Syne / Inter | none | violet atmospheric glow | 24px |
| Y2K | Outfit | 2px light | gloss + cyan haze | pill |
| Pixel Art | Press Start 2P / VT323 | 4px stepped | stepped pixel shadow | 0 |
| Synthwave | Orbitron / Inter | 1px magenta | dual neon glow | 6px |
| Glassmorphism | Inter | 1px slate | blur + soft shadow | 20px |
| Neumorphism | Inter | 1px on controls only | twin soft shadows | 16px |
| Bento Grid | Plus Jakarta Sans / Inter | 1px (decorative edge) | subtle | 20px |
| Editorial | Playfair Display / Newsreader | rules | none | 0 |
| Swiss | Inter | 2–4px rules | none | 0 |
| Minimalism | Inter | 1px on controls | none | 6px |
| Maximalism | Anton / Inter | heavy | offset magenta | 0 |
| Luxury Typography | Bodoni Moda / Cormorant Garamond | 1px dark gold | none | 0 |
| Conceptual Sketch | Architects Daughter / Inter | 2px rough | none | hand-drawn |
| Ethereal | Cormorant Garamond / Urbanist | 1px lavender grey | pastel haze | 24px |
| Bohemian | Fraunces / Lora | 1px warm | soft organic | 12px |
| Victorian | Cinzel Decorative / Lora | 4px double | inset vignette | 2px |
| Cyberpunk | Rajdhani / Chakra Petch | 1px yellow (drawn) | drop-shadow glow | cut corners |
| Wabi-Sabi | Shippori Mincho / Cormorant Garamond | 1px raw | soft natural | 4px |

---

## 1. Neo-Brutalism

### Vanilla CSS
```css
.nb-card {
  background: var(--ui-surface);
  color: var(--ui-text);
  border: 3px solid var(--ui-border);
  border-radius: var(--ui-radius);
  box-shadow: var(--ui-shadow);
  padding: 24px;
}
.nb-button {
  background: var(--ui-accent);
  color: var(--ui-on-accent);
  font: 700 1rem/1.2 var(--ui-font-display);
  border: 3px solid var(--ui-border);
  border-radius: var(--ui-radius);
  box-shadow: 4px 4px 0 var(--ui-border);
  min-height: 44px;
  padding: 10px 24px;
  cursor: pointer;
  transition: transform 0.12s ease, box-shadow 0.12s ease;
}
.nb-button:hover  { transform: translate(2px, 2px); box-shadow: 2px 2px 0 var(--ui-border); }
.nb-button:active { transform: translate(4px, 4px); box-shadow: none; }
.nb-input {
  background: var(--ui-surface);
  color: var(--ui-text);
  border: 3px solid var(--ui-border);
  border-radius: var(--ui-radius);
  min-height: 44px;
  padding: 8px 12px;
  font: 1rem var(--ui-font-body);
}
/* focus: SKILL.md §5.1. Add data-ui-motion to .nb-button so reduced motion drops the press offset. */
```

### Tailwind (v4 with the `@theme inline` mapping from SKILL.md §2)
```html
<div class="theme-neo-brutalism bg-ui-surface text-ui-text border-[3px] border-ui-border rounded-ui shadow-ui p-6 font-ui-body">
  <h3 class="font-ui-display font-bold text-xl mb-2">Neo-Brutalism card</h3>
  <p class="text-ui-muted mb-4">High contrast, raw, unapologetically functional.</p>
  <button data-ui-motion class="bg-ui-accent text-ui-on-accent font-ui-display font-bold min-h-11 px-6 py-2.5 rounded-ui border-[3px] border-ui-border shadow-[4px_4px_0_var(--ui-border)]
           hover:translate-x-0.5 hover:translate-y-0.5 hover:shadow-[2px_2px_0_var(--ui-border)] active:translate-x-1 active:translate-y-1 active:shadow-none
           motion-reduce:translate-none transition focus-visible:outline-3 focus-visible:outline-offset-3 focus-visible:outline-ui-focus">
    Execute action
  </button>
</div>
```

---

## 2. Glassmorphism

Use only over a dark or saturated backdrop. The surface tint keeps white text at **7.95:1** even if the area behind it is pure white. The button sits at **5.76:1** at rest and **4.70:1** on hover, all computed against `#ffffff` as the worst case.

### Vanilla CSS
```css
.glass-card {                       /* add class ui-glass for the §5.3 fallbacks */
  background: var(--ui-surface);    /* rgba(15, 23, 42, 0.75) */
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.25);   /* decorative hairline */
  border-radius: var(--ui-radius);
  box-shadow: var(--ui-shadow);
  color: var(--ui-text);
  padding: 24px;
}
.glass-button {
  background: rgba(255, 255, 255, 0.12);
  color: var(--ui-text);
  border: 1px solid var(--ui-border);
  border-radius: 9999px;
  min-height: 44px;
  padding: 10px 20px;
  font-weight: 500;
  cursor: pointer;
  transition: background 0.2s ease;
}
.glass-button:hover { background: rgba(255, 255, 255, 0.20); }   /* do not go above 0.20: contrast drops below 4.5:1 */
.glass-input {
  background: rgba(15, 23, 42, 0.6);
  color: var(--ui-text);
  border: 1px solid var(--ui-border);
  border-radius: 12px;
  min-height: 44px;
  padding: 8px 12px;
}
```

### Tailwind (v4)
```html
<div class="theme-glassmorphism ui-glass bg-ui-surface backdrop-blur-lg border border-white/25 rounded-ui shadow-ui p-6 text-ui-text">
  <h3 class="text-xl font-semibold mb-2">Glassmorphism card</h3>
  <p class="text-ui-muted mb-4">Translucent layers with crisp edge highlights.</p>
  <button class="bg-white/12 hover:bg-white/20 border border-ui-border rounded-full min-h-11 px-5 py-2 font-medium transition
                 focus-visible:outline-3 focus-visible:outline-offset-3 focus-visible:outline-ui-focus">Discover more</button>
</div>
```

---

## 3. Bento Grid

### Vanilla CSS
```css
.bento {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
  grid-auto-rows: minmax(12rem, auto);
  gap: 16px;
}
.bento-card {
  background: var(--ui-surface);
  color: var(--ui-text);
  border: 1px solid #e4e4e7;          /* decorative card edge */
  border-radius: var(--ui-radius);
  box-shadow: var(--ui-shadow);
  padding: 24px;
}
@media (min-width: 48rem) { .bento-card--hero { grid-column: span 2; grid-row: span 2; } }
.bento-input { border: 1px solid var(--ui-border); }   /* inputs use the 3:1 border, never the decorative edge */
```

### Tailwind (v4)
```html
<div class="theme-bento-grid grid grid-cols-1 md:grid-cols-3 gap-4 max-w-5xl mx-auto bg-ui-bg p-4">
  <div class="md:col-span-2 md:row-span-2 bg-ui-surface border border-zinc-200 rounded-ui p-8 text-ui-text flex flex-col justify-between">
    <div>
      <span class="text-xs uppercase tracking-wider text-ui-muted font-semibold">Real-time telemetry</span>
      <h2 class="text-2xl font-bold mt-1 font-ui-display">Unified data stream</h2>
    </div>
    <div class="h-32 bg-ui-bg rounded-2xl border border-zinc-200 grid place-items-center text-ui-muted">Chart area</div>
  </div>
  <div class="bg-ui-surface border border-zinc-200 rounded-ui p-6 text-ui-text">
    <span class="text-ui-muted text-xs font-semibold">Uptime</span>
    <div class="text-3xl font-extrabold">99.98%</div>
  </div>
  <div class="bg-ui-surface border border-zinc-200 rounded-ui p-6 text-ui-text">
    <span class="text-ui-muted text-xs font-semibold">Latency</span>
    <div class="text-3xl font-extrabold">&lt; 14ms</div>
  </div>
</div>
```

---

## 4. Cyberpunk (cut corners without clipping focus)

`clip-path` clips everything outside its path, including the element's own `box-shadow` and focus outline. So the focusable element is **never** clipped. Its cut shape is drawn by pseudo-elements behind the content, and the glow is a `filter: drop-shadow` that follows that shape.

Contrast: the card's yellow text on `#0d0d11` is 16.04:1. The black label is 17.37:1 on yellow and 14.91:1 on cyan when hovered.

```css
.cyber-card, .cyber-btn {
  position: relative;
  isolation: isolate;               /* keeps the z-index:-1 layers inside the element */
  background: none;                 /* never set a rectangular background here */
  filter: drop-shadow(0 0 8px rgba(252, 238, 9, 0.35));
}
.cyber-card::before, .cyber-card::after,
.cyber-btn::before {
  content: "";
  position: absolute;
  z-index: -1;
  --cut: 16px;
  clip-path: polygon(0 0, calc(100% - var(--cut)) 0, 100% var(--cut), 100% 100%, var(--cut) 100%, 0 calc(100% - var(--cut)));
}
/* Card: yellow outer layer = border, dark inner layer = fill */
.cyber-card { color: var(--ui-text); padding: 24px; }
.cyber-card::before { inset: 0;   background: var(--ui-border); }
.cyber-card::after  { inset: 1px; background: var(--ui-surface); }

/* Button: one yellow layer, black label */
.cyber-btn {
  color: var(--ui-on-accent);
  border: 0;
  font: 700 1rem/1 var(--ui-font-display);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  min-height: 44px;
  padding: 12px 28px;
  cursor: pointer;
}
.cyber-btn::before { inset: 0; --cut: 10px; background: var(--ui-accent); transition: background 0.2s ease; }
.cyber-btn:hover::before { background: #00f0ff; }
.cyber-btn:focus-visible { outline: 2px solid var(--ui-focus); outline-offset: 4px; }   /* visible: the element itself is not clipped */
.cyber-input {
  background: var(--ui-surface);
  color: var(--ui-text);
  border: 1px solid var(--ui-border);
  min-height: 44px;
  padding: 8px 12px;
  font: 1rem var(--ui-font-body);
}
```

---

## 5. Swiss Design

```css
.swiss-container {
  background: var(--ui-bg);
  color: var(--ui-text);
  font-family: var(--ui-font-body);   /* "Helvetica Neue" may be prepended as an optional local match */
  border-top: 4px solid #ff0000;      /* decorative Swiss red: rules and blocks only */
  padding: 40px;
}
.swiss-header {
  font: 800 clamp(2.25rem, 5vw, 3.5rem)/0.95 var(--ui-font-display);
  letter-spacing: -0.04em;
  text-transform: uppercase;          /* headings only */
  margin-bottom: 24px;
}
.swiss-link { color: var(--ui-accent); }   /* #d00000 — use this red for text, never #ff0000 (4.0:1) */
.swiss-rule { border: 0; border-top: 2px solid var(--ui-border); margin: 32px 0; }
.swiss-button { background: var(--ui-accent); color: var(--ui-on-accent); border: 0; min-height: 44px; padding: 10px 24px; font-weight: 700; }
.swiss-input  { border: 2px solid var(--ui-border); min-height: 44px; padding: 8px 12px; }
```

---

## 6. Wabi-Sabi

```css
.wabi-container {
  background: var(--ui-bg);
  color: var(--ui-text);
  font-family: var(--ui-font-body);
  padding: 48px;
  line-height: 1.85;
}
.wabi-card {
  background: var(--ui-surface);
  border-bottom: 1px solid rgba(35, 35, 35, 0.2);   /* decorative divider */
  border-radius: var(--ui-radius);
  box-shadow: var(--ui-shadow);
  padding: 24px;
  margin-bottom: 32px;
}
.wabi-title { font: 400 1.75rem var(--ui-font-display); letter-spacing: 0.05em; }
.wabi-button { background: var(--ui-accent); color: var(--ui-on-accent); border: 0; border-radius: var(--ui-radius); min-height: 44px; padding: 10px 24px; }
.wabi-input  { background: var(--ui-surface); border: 1px solid var(--ui-border); border-radius: var(--ui-radius); min-height: 44px; padding: 8px 12px; }
```
