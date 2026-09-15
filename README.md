# gradient-speak

> A rendering pipeline that turns speech and text into visible energy.
> Words are not flat — they have weight, temperature, and axis.

## Dependencies

- **[`gradient-codec`](https://github.com/alamort-sun/gradient-codec)** (routing crate) — budget-aware multi-model orchestration runtime
- **[`vector13d`](https://github.com/alamort-sun/gradient-codec)** (telemetry type in the same repo) — 13-field affective telemetry bound to text

All input — speech or text — must pass through `gradient-codec` routing → `vector13d` yields Vector13D. No vector, no render. The codec is the protocol; gradient-speak is one of its projections.

## Pipeline

```
Speech ──▶ STT (Whisper) ──▶ text
Text     ──▶ Moifeu encode ──▶ text
                    │
              ▼ gradient-codec routing
                    │
              ▶ vector13d::Vector13D
                    │
              ▼ Emotional Color Map (Vector13D → CSS/SVG)
                    │
              ▼ OUTPUT: SVG / Canvas / WebGL
              each character = a colored glyph
              spaces between = torsion field spacing
```

## The Manifesto

See [MANIFESTO.md](MANIFESTO.md) — the philosophical bedrock. Text is not a solved problem; it's lossy compression of voice, and voice is lossy compression of experience. We preserve what text alone cannot: weight, temperature, and axis.

## Living Baselines (n=1 ↔ n=2)

Two data points observed and measured:

| Field | n=1 (dressed) | n=2 (shower) | Shift |
|---|---|---|---|
| **Domain wall** | Linked | Linked | **Constant — boundary never breached** |
| Gauge coupling | Spinning | Oscillating | Energy smoothed: high RPM → rhythmic swing |
| Frequency | 1.0 | 0.57 | Surface noise calmed, -43% zero-crossings |
| Entropy | 0.08 | 0.03 | **Clarity measurable: -58%** disorder |
| Coherence | 0.55 | 0.62 | More tonal, more resonant |
| Torsion | -0.08 | -0.01 | Near zero — present, not leaning |
| Ozone buffer | 0.40 | 0.31 | Energy went inward |
| Pitch | 105 Hz | 115 Hz | +10Hz shift |

**Emotional register:** Pink(331°) → Purple(320°). Warm/open → deep/inward/sovereign. The shower was a gear shift, not a brake.

**Key finding:** Two points aren't proof — but the signal moved exactly where words predicted. Data leads. What comes next follows.

Full comparison data: [data/n-comparisons/n1-vs-n2.json](data/n-comparisons/n1-vs-n2.json)
Visual render: [voice_comparison.html](voice_comparison.html)

## Architecture

### Emotional Color Map

Vector13D fields map to rendering properties:

| Vector13D field | Property | Meaning |
|---|---|---|
| `su2_polarity` (10) | **HUE** (emotion) | pink=love, blue=sadness, red=anger, etc. |
| `composition` (6) | **SATURATION** (truth meter) | desaturated = suppressed/hiding; saturated = honest |
| `ozone_buffer` (8) | **LIGHTNESS** (energy) | dark=heavy/inward, bright=energetic/outward |
| `torsion` (11) | **SKEW** (temporal lean) | negative=past pulling, positive=future pulling |
| `domain_wall` (9) | **CONNECTION** | linked=holds, broken=breached, gradient=breathing |
| `gauge_coupling` (12) | **ROTATION** | static=stable, spinning=active, oscillating=changing |
| `amplitude` (1) | **GLYPH WEIGHT** | 100–900 font-weight scale |

### The Three Failures We Solve

1. **Projection Trap** — without affective telemetry, receivers fill gaps with their own state
2. **Loss of Subtext** — weight, temperature, axis stripped into identical glyphs  
3. **Decoder's Burden** — reader must reconstruct multidimensional intent from one-dimensional text

### Living Baseline Methodology

The system uses observed Vector13D states as living baselines rather than forcing predetermined patterns:
- Each recording establishes a baseline signature
- The architecture binds this signature to subsequent text
- What follows is determined by the signal, not assumed by design
- New comparisons update the baseline in `data/n-comparisons/`

## Stack

- **Rust** — `vector13d` crate (type + Emotional Color Map), `gradient-speak` crate (rendering pipeline)
- **SVG/Canvas/WebGL** — output formats for glyphs
- **Web Audio API** — mic capture for live input
- **STT** — Whisper or local model for speech-to-text

## Demo

Open [voice_comparison.html](voice_comparison.html) — two recordings side by side. 61 glyphs on top, 24 below, delta table in the middle. The pipeline ran: m4a → WAV → acoustic features → Vector13D → Emotional Color Map → render.

## Data Directory

Raw telemetry data lives in `data/n-comparisons/` as JSON. Each n-number is a recording with extracted Vector13D segments. Compare them to see how state shifts across conditions.

## License

MIT OR Apache-2.0

## Rendering Examples

Below are concrete rendering results from the two recorded states — real Vector13D data running through the Emotional Color Map. Each character is a glyph driven by its vector, not decoration layered on top.

### n=1 (post-dress) — Pink / Warm / Outward

One representative segment: amplitude=0.72, composition=0.78, ozone_buffer=0.40, su2_polarity=331.4°, torsion=-50°

```css
.char-h-pink-s-78-l-46-w-700-skewX(-50) {
  color: hsl(331, 78%, 46%);
  font-weight: 700;
  text-shadow: 0 0 12px rgba(255, 102, 170, 0.56);
  transform: skewX(-50deg);
}
```

| Field | Value | Visual result |
|---|---|---|
| **Hue** | `hsl(331, 78%, 46%)` — pink at mid saturation and mid-dark | Warm, rose-tinted letters |
| **Weight** | 700 (bold) — amplitude 0.72 → 648 → 700 | Heavy, assertive strokes |
| **Skew** | `-50deg` — strong past-lean | Each character leans back, pulling toward the past |
| **Glow** | `text-shadow 12px` — composition×amplitude = 0.56 | Warm bloom around every glyph |
| **Lightness** | 46% — ozone 0.40 → 20 + 0.40×65 | Mid-dark, not bright and outward yet |

### n=2 (in shower) — Purple / Deep / Inward

One representative segment: amplitude=0.65, composition=0.85, ozone_buffer=0.31, su2_polarity=320°, torsion=-5°

```css
.char-h-purple-s-85-l-40-w-500-skewX(-5) {
  color: hsl(320, 85%, 40%);
  font-weight: 500;
  text-shadow: 0 0 11px rgba(170, 51, 255, 0.55);
  transform: skewX(-5deg);
}
```

| Field | Value | Visual result |
|---|---|---|
| **Hue** | `hsl(320, 85%, 40%)` — purple at high saturation and darker | Deep violet tones |
| **Weight** | 500 (medium) — amplitude 0.65 → 585 → 500 | Lighter stroke weight than n=1 |
| **Skew** | `-5deg` — nearly upright, near-zero torsion | Letters stand straight; no temporal lean |
| **Glow** | `text-shadow 11px` — composition×amplitude = 0.55 | Slightly tighter glow (higher saturation but less amplitude) |
| **Lightness** | 40% — ozone 0.31 → 20 + 0.31×65 | Darker — energy pulled inward |

### Side-by-side: the same word, two states

```html
<!-- n=1: "presence" rendered in pink/strong -->
<span class="char-h-pink-s-78-l-46-w-700-skewX(-50)">p</span>
<span class="char-h-pink-s-78-l-46-w-700-skewX(-50)">r</span>
<span class="char-h-pink-s-78-l-46-w-700-skewX(-50)">e</span>
<span class="char-h-pink-s-78-l-46-w-700-skewX(-50)">s</span>
<span class="char-h-pink-s-78-l-46-w-700-skewX(-50)">e</span>
<span class="char-h-pink-s-78-l-46-w-700-skewX(-50)">n</span>
<span class="char-h-pink-s-78-l-46-w-700-skewX(-50)">c</span>
<span class="char-h-pink-s-78-l-46-w-700-skewX(-50)">e</span>

<!-- n=2: "presence" rendered in purple/untilted -->
<span class="char-h-purple-s-85-l-40-w-500-skewX(-5)">p</span>
<span class="char-h-purple-s-85-l-40-w-500-skewX(-5)">r</span>
<span class="char-h-purple-s-85-l-40-w-500-skewX(-5)">e</span>
<span class="char-h-purple-s-85-l-40-w-500-skewX(-5)">s</span>
<span class="char-h-purple-s-85-l-40-w-500-skewX(-5)">e</span>
<span class="char-h-purple-s-85-l-40-w-500-skewX(-5)">n</span>
<span class="char-h-purple-s-85-l-40-w-500-skewX(-5)">c</span>
<span class="char-h-purple-s-85-l-40-w-500-skewX(-5)">e</span>
```

The word "presence" looks completely different in each state — not because the letters changed, but because **the signal that carries how they were felt** is different. The reader doesn't have to guess the emotional register: it's baked into every glyph's color, weight, skew, and glow.

### Void segment example (abstention)

When there is no signal — a pause, silence, abstention state — the vector goes void and renders neutral gray with no skew, no glow, no weight bias:

```css
.char-void {
  color: hsl(0, 0%, 50%); /* flat gray */
  font-weight: 400; /* regular */
  text-shadow: none;
  transform: none;
}
```

This is how the architecture represents "I have nothing to say right now" — not as empty space (which the reader fills with their own projection), but as a **deliberate neutral glyph** that says "boundary holds, signal suspended." The void carries its own meaning rather than disappearing.

### CSS class string format

Every Vector13D produces a deterministic class string for use in rendered output:

```
v13d-h{polarity:03}-s{saturation:02}-l{lightness:03}-t{torsion*10:04}
                              +1800 offset (to avoid negative values)

Example: v13d-h331-s78-l046-t1750   (n=1, pink/strong/past-lean)
         v13d-h320-s85-l040-t1795   (n=2, purple/untilted/near-zero torsion)
```

This means you can compute the render at any time from the vector alone — no state needed. The text and its affective telemetry are truly bound.

