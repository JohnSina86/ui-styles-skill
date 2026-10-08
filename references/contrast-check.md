# Contrast check

A copy-paste function that computes a pair the way [contrast-ledger.md](contrast-ledger.md) does: linearise sRGB, compute WCAG relative luminance, composite a translucent foreground over its backdrop first, and print **both luminances beside the ratio**, as the contract in `SKILL.md` §4 requires. Use it instead of doing the arithmetic by hand. It doesn't change the rules: a ledger row still covers only the exact foreground, background and state it names, and a colour reused on another surface is a new pair.

Run it in Node or a browser console. It reads nothing and writes nothing.

```js
function contrast(fg, bg, alpha = 1) {
  /* Accepts #rgb, #rgba, #rrggbb and #rrggbbaa. Anything else throws rather than returning a
     misleading number. A foreground's own alpha multiplies `alpha`; the background must be opaque. */
  const parse = (hex, role) => {
    const m = /^#?([0-9a-f]{3,4}|[0-9a-f]{6}|[0-9a-f]{8})$/i.exec(String(hex).trim());
    if (!m) throw new Error(`${role}: "${hex}" is not #rgb, #rgba, #rrggbb or #rrggbbaa`);
    const v = m[1].length <= 4 ? m[1].replace(/./g, c => c + c) : m[1];
    const ch = [0, 2, 4, 6].map(i => parseInt(v.slice(i, i + 2), 16));
    return { rgb: ch.slice(0, 3), a: v.length === 8 ? ch[3] / 255 : 1 };
  };
  if (typeof alpha !== 'number' || !Number.isFinite(alpha) || alpha < 0 || alpha > 1) throw new Error(`alpha must be a number from 0 to 1, got ${alpha}`);
  const f = parse(fg, 'foreground'), b = parse(bg, 'background');
  if (b.a < 1) throw new Error('background must be opaque: composite it over what sits beneath it first');
  const a = alpha * f.a;
  const top = f.rgb.map((c, i) => Math.round(a * c + (1 - a) * b.rgb[i]));   // ledger method, step 4
  const lum = ([r, g, bl]) => { const lin = c => { c /= 255; return c <= 0.04045 ? c / 12.92 : ((c + 0.055) / 1.055) ** 2.4; };
    return 0.2126 * lin(r) + 0.7152 * lin(g) + 0.0722 * lin(bl); };
  const [L1, L2] = [lum(top), lum(b.rgb)];
  const ratio = (Math.max(L1, L2) + 0.05) / (Math.min(L1, L2) + 0.05);
  return `L1 ${L1.toFixed(4)}, L2 ${L2.toFixed(4)} -> ${ratio.toFixed(2)}:1`;
}
```

Examples, which reproduce the ledger:
- `contrast('#000000', '#ffffff')` gives `L1 0.0000, L2 1.0000 -> 21.00:1`.
- `contrast('#0f172a', '#ffffff', 0.75)` gives `L1 0.0821, L2 1.0000 -> 7.95:1`, the worked example `D-glass-card-text` in the ledger's Method. `contrast('#0f172abf', '#ffffff')` gives the same result, because `bf` is 0.75 alpha.
- `contrast('#00000000', '#ffffff')` gives `1.00:1`: a fully transparent foreground disappears into its background.

It throws, rather than guessing, on a malformed colour, on an alpha outside 0–1, and on a translucent background. To use a translucent background, composite it over what sits beneath it first, then pass the result as `bg`. Quote the printed line as it stands: the luminances are what make the ratio checkable.
