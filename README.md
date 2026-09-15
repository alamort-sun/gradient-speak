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

### How: Affective Telemetry Layer

Text and Vector13D are bound as a co-equal channel:
- Each character has its own vector carrying *how* the words were felt
- The binding is immutable — separating vector from text destroys meaning
- Rendering uses the vector to drive color, weight, skew, glow, connection state
- Void segments (abstentions) render as neutral gray with no skew

## Stack

- **Rust** — `vector13d` crate (type + Emotional Color Map), `gradient-speak` crate (rendering pipeline)
- **SVG/Canvas/WebGL** — output formats for glyphs
- **Web Audio API** — mic capture for live input
- **STT** — Whisper or local model for speech-to-text

## Demo

Open [voice_demo.html](voice_demo.html) — your voice, rendered as 61 glyphs of visible energy. The pipeline ran: m4a → WAV → acoustic features → Vector13D → Emotional Color Map → SVG/Canvas render.

## License

MIT OR Apache-2.0
