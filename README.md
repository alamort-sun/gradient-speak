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
