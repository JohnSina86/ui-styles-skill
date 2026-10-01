# UI Styles & Visual Themes: Complete Component Catalog

This catalog provides copy-paste ready HTML, Vanilla CSS, and Tailwind CSS recipes for the 22 visual design styles.

---

## Quick Component Matrix

| Style | Primary Font | Border | Key Elevation / Shadow | Corner Radius |
| :--- | :--- | :--- | :--- | :--- |
| **Claymorphism** | Poppins / Nunito | None | 4-layer inner + outer shadows | 24px–32px |
| **Cybercore** | JetBrains Mono | 1px Cyan/Slate | Inset cyan glow | 0px–2px |
| **Neo-Brutalism** | Space Grotesk / Lexend | 2px–4px Black | Solid 4px–6px offset (no blur) | 0px or 6px–8px |
| **Scrapbook** | Caveat / Patrick Hand | 1px sepia border | Subtle drop shadow + -2deg tilt | 2px–4px |
| **Surrealism** | Syne / Cormorant | None | Colored atmospheric glow | 16px–32px |
| **Y2K Aesthetic** | Dela Gothic One / Outfit | 2px glossy border | Specular shine + outer cyan haze | Pill (9999px) |
| **Pixel Art** | Press Start 2P / Silkscreen | 4px stepped block | Stepped pixel shadow | 0px |
| **Synthwave** | Orbitron / Montserrat | 1px Neon Magenta | Neon magenta/cyan dual glow | 4px–8px |
| **Glassmorphism** | Inter / SF Pro | 1px 20% white | Backdrop blur (16px) + soft shadow | 16px–24px |
| **Neumorphism** | Inter / Roboto | None | Twin soft light & dark shadows | 16px–20px |
| **Bento Grid** | Plus Jakarta Sans / Inter | 1px zinc-200 | Soft diffuse shadow (sm/md) | 20px–24px |
| **Editorial** | Playfair Display / Newsreader | 1px–2px black rule | None (rely on typographic rules) | 0px |
| **Swiss Design** | Helvetica Neue / Inter | 2px–3px black rule | Flat (no shadows) | 0px |
| **Minimalism** | Inter / Geist | 1px light gray | Extremely subtle or none | 4px–8px |
| **Maximalism** | Clash Display / Anton | Heavy clashing | Harsh offset colored shadows | Mixed / Wild |
| **Luxury Typography** | Bodoni Moda / Cormorant | 1px pale gold | None (flat elegance) | 0px–2px |
| **Conceptual Sketch** | Architects Daughter / Kalam | 2px rough outline | Minimalist blueprint grid | Asymmetric hand-drawn |
| **Ethereal** | Cormorant / Urbanist | 1px frosted white | Multi-colored pastel haze | 20px–30px |
| **Bohemian** | Fraunces / Lora | 1px warm sand | Soft organic shadow | 8px–16px |
| **Victorian** | Cinzel Decorative / IM Fell | Double / Filigree | Inset aged vignette shadow | 0px–4px |
| **Cyberpunk** | Rajdhani / Chakra Petch | 1px–2px Neon Yellow | Clipped polygonal corners + glow | Cut-angle polygon |
| **Wabi-Sabi** | Noto Serif / Shippori Mincho | Subtle 1px raw border| Soft natural drop shadow | Organic / Asymmetric |

---

## Detailed Component Recipes

### 1. Neo-Brutalism

#### Vanilla CSS
```css
/* Card */
.nb-card {
  background-color: #ffffff;
  border: 3px solid #000000;
  border-radius: 8px;
  box-shadow: 5px 5px 0px #000000;
  padding: 24px;
}

/* Button */
.nb-button {
  background-color: #ffde59;
  color: #000000;
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 700;
  border: 2px solid #000000;
  border-radius: 6px;
  box-shadow: 4px 4px 0px #000000;
  padding: 12px 24px;
  cursor: pointer;
  transition: all 0.15s ease-in-out;
}
.nb-button:hover {
  transform: translate(2px, 2px);
  box-shadow: 2px 2px 0px #000000;
}
.nb-button:active {
  transform: translate(4px, 4px);
  box-shadow: 0px 0px 0px #000000;
}
```

#### Tailwind CSS
```html
<!-- Card -->
<div class="bg-white border-2 border-black rounded-lg shadow-[4px_4px_0px_0px_rgba(0,0,0,1)] p-6">
  <h3 class="font-bold text-xl mb-2 font-mono">Neo-Brutalism Card</h3>
  <p class="text-zinc-700 mb-4">High-contrast, raw, and unapologetically functional.</p>
  
  <!-- Button -->
  <button class="bg-[#FFDE59] text-black font-bold px-5 py-2.5 rounded-md border-2 border-black shadow-[3px_3px_0px_0px_rgba(0,0,0,1)] hover:translate-x-[2px] hover:translate-y-[2px] hover:shadow-[1px_1px_0px_0px_rgba(0,0,0,1)] active:translate-x-[3px] active:translate-y-[3px] active:shadow-none transition-all">
    Execute Action
  </button>
</div>
```

---

### 2. Glassmorphism

#### Vanilla CSS
```css
/* Frosted Glass Card */
.glass-card {
  background: rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.25);
  border-radius: 20px;
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.15);
  padding: 24px;
  color: #ffffff;
}

/* Glass Button */
.glass-button {
  background: rgba(255, 255, 255, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.4);
  backdrop-filter: blur(8px);
  border-radius: 9999px;
  color: #ffffff;
  padding: 10px 20px;
  font-weight: 500;
  transition: background 0.2s ease, border-color 0.2s ease;
}
.glass-button:hover {
  background: rgba(255, 255, 255, 0.35);
  border-color: rgba(255, 255, 255, 0.6);
}
```

#### Tailwind CSS
```html
<div class="bg-white/10 backdrop-blur-md border border-white/20 rounded-2xl shadow-xl p-6 text-white">
  <h3 class="text-xl font-semibold mb-2">Glassmorphism Card</h3>
  <p class="text-white/80 mb-4">Translucent layers with crisp specular edge highlights.</p>
  <button class="bg-white/20 hover:bg-white/30 border border-white/30 rounded-full px-5 py-2 font-medium transition">
    Discover More
  </button>
</div>
```

---

### 3. Bento Grid

#### Vanilla CSS & Grid Template
```css
.bento-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 200px;
  gap: 16px;
}

.bento-card-large {
  grid-column: span 2;
  grid-row: span 2;
  background: #ffffff;
  border: 1px solid #e4e4e7;
  border-radius: 24px;
  padding: 28px;
}

.bento-card-compact {
  grid-column: span 1;
  background: #f4f4f5;
  border: 1px solid #e4e4e7;
  border-radius: 20px;
  padding: 20px;
}
```

#### Tailwind CSS
```html
<div class="grid grid-cols-1 md:grid-cols-3 gap-4 max-w-5xl mx-auto">
  <!-- Large Hero Card -->
  <div class="md:col-span-2 md:row-span-2 bg-zinc-900 border border-zinc-800 rounded-3xl p-8 text-white flex flex-col justify-between">
    <div>
      <span class="text-xs uppercase tracking-wider text-zinc-400 font-semibold">Real-time Telemetry</span>
      <h2 class="text-2xl font-bold mt-1">Unified Data Stream</h2>
    </div>
    <div class="h-32 bg-zinc-800/60 rounded-2xl border border-zinc-700/50 flex items-center justify-center text-zinc-500">
      Chart / Widget Area
    </div>
  </div>

  <!-- Secondary Tile -->
  <div class="bg-zinc-900/50 border border-zinc-800 rounded-3xl p-6 text-white flex flex-col justify-between">
    <span class="text-zinc-400 text-xs font-semibold">Speed</span>
    <div class="text-3xl font-extrabold text-emerald-400">99.98%</div>
  </div>

  <!-- Secondary Tile -->
  <div class="bg-zinc-900/50 border border-zinc-800 rounded-3xl p-6 text-white flex flex-col justify-between">
    <span class="text-zinc-400 text-xs font-semibold">Latency</span>
    <div class="text-3xl font-extrabold text-cyan-400">&lt; 14ms</div>
  </div>
</div>
```

---

### 4. Cyberpunk

#### Vanilla CSS
```css
/* Cut-Corner Angular Card */
.cyber-card {
  background: #0d0d11;
  border: 1px solid #fcee09;
  clip-path: polygon(0 0, calc(100% - 16px) 0, 100% 16px, 100% 100%, 16px 100%, 0 calc(100% - 16px));
  box-shadow: 0 0 15px rgba(252, 238, 9, 0.2);
  padding: 24px;
  color: #fcee09;
}

/* Cyber Button */
.cyber-btn {
  background: #fcee09;
  color: #000000;
  font-family: 'Rajdhani', sans-serif;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  padding: 10px 24px;
  clip-path: polygon(10px 0, 100% 0, calc(100% - 10px) 100%, 0 100%);
  border: none;
  cursor: pointer;
  transition: all 0.2s ease;
}
.cyber-btn:hover {
  background: #00f0ff;
  box-shadow: 0 0 12px #00f0ff;
}
```

---

### 5. Swiss Design

#### Vanilla CSS
```css
.swiss-container {
  font-family: 'Helvetica Neue', Arial, sans-serif;
  background: #ffffff;
  color: #000000;
  border-top: 4px solid #ff0000; /* Swiss Red accent */
  padding: 40px;
}

.swiss-header {
  font-size: 3.5rem;
  font-weight: 800;
  letter-spacing: -0.04em;
  line-height: 0.95;
  text-transform: uppercase;
  margin-bottom: 24px;
}

.swiss-rule {
  border: none;
  border-top: 2px solid #000000;
  margin: 32px 0;
}
```

---

### 6. Wabi-Sabi

#### Vanilla CSS
```css
.wabi-container {
  background: #edeae1;
  color: #2b2927;
  font-family: 'Cormorant Garamond', 'Noto Serif JP', serif;
  padding: 48px;
  line-height: 1.85;
}

.wabi-card {
  border-bottom: 1px solid rgba(43, 41, 39, 0.2);
  padding-bottom: 24px;
  margin-bottom: 32px;
}

.wabi-title {
  font-size: 1.75rem;
  font-weight: 400;
  letter-spacing: 0.05em;
  color: #1a1816;
}
```
