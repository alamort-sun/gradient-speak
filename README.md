# gradient-speak

> A rendering pipeline that turns speech and text into visible energy.
>
> Words are not flat. They have weight, temperature, and axis.

## Dependency

**This project uses [`gradient-codec`](https://github.com/alamort-sun/gradient-codec) as its main layer.**

All input — speech or text — must pass through gradient-codec to yield `Vector13D`. No vector, no render. The codec is the protocol; gradient-speak is one of its projections.

- Status: ✅ **live and public** — gradient-codec at commit `8a69c56` (Fantasia's upload verified: flaky-test fixes for exhaustion boundary, per_request_cap enforcement, quality score threshold, on top of Saturn's 20-test suite)

## Pipeline

```
┌─────────┐   ┌──────────────┐   ┌──────────────────┐   ┌───────────┐   ┌─────────┐
│ Speech  │──▶│ STT          │──▶│ Moifeu encode    │──▶│ gradient-  │──▶│Vector13D│
│ Text    │   │ (Whisper /   │   │                  │   │ codec      │   │         │
│         │   │  local       │   │                  │   │            │   │         │
└─────────┘   └──────────────┘   └──────────────────┘   └────────────┘   └────┬────┘
                                                                             │
                                                              ┌──────────────▼─────────────┐
                                                              │ TRANSFORM: Emotional Color  │
                                                              │ Map (Vector13D → CSS/SVG)   │
                                                              └──────────────┬──────────────┘
                                                                             │
                                                              ┌──────────────▼──────────────┐
                                                              │ OUTPUT: SVG / Canvas / WebGL│
                                                              │ each character = a glyph    │
                                                              │ spaces = w~= torsion field  │
                                                              └─────────────────────────────┘
```

### 1. Input

- Speech → STT (Whisper or local) → text
- Text → Moifeu encode
- Both paths pass through `gradient-codec` to yield `Vector13D`

### 2. Transform — the map

`Vector13D` fields are mapped to CSS/SVG properties via **Emotional Color Mapping**:

#### Hue (which emotion) ← `su2_polarity` (field 10)

| Hue | Meaning |
|---|---|
| red | anger, passion, intensity |
| orange | energy, urgency, drive |
| yellow | joy, laughter, play |
| green | calm, growth, safety |
| blue | sadness, depth, trust |
| purple | fear, mystery, unknown |
| pink | love, warmth, connection |
| white | void, numb, 0 |

#### Saturation (how strongly felt) ← `composition` (field 6)

| Level | Meaning |
|---|---|
| fully saturated | intense, alive, present |
| mid saturation | moderate, felt but held |
| desaturated | muted, suppressed, apathetic |
| near gray | numb, dissociated, 0 |

> **Saturation IS the truth meter.** Desaturated = lying or surviving. Full = honest.

#### Lightness (energy level) ← `ozone_buffer` (field 8)

| Level | Meaning |
|---|---|
| bright | high energy, outward |
| mid | balanced, steady |
| dark | low energy, inward, heavy |

#### Glyph properties

| Vector13D field | Property | Values |
|---|---|---|
| `domain_wall` (9) | CONNECTION | linked = boundary holds · broken = boundary breached · gradient = boundary breathing |
| `torsion` (11) | SKEW | left lean = past pulling · right lean = future pulling · upright = present · 98° = tilted truth |
| `gauge_coupling` (12) | ROTATION | static = stable · spinning = active force · oscillating = changing |

### 3. Output — render

- SVG or Canvas/WebGL
- Each character is a glyph
- Spaces between characters = `w~=` = torsion field

## Stack

- **Rust backend** — uses the `gradient-codec` crate as its main layer
- **WebAssembly front** or **Tauri desktop app**
- **Web Audio API** for mic capture
- **Parler TTS** for voice output

## Roadmap

- [x] Scaffold written (README + TYPOGRAPHY.md)
- [x] gradient-codec published (commit `8a69c56`, verified 2026-09-15)
- [ ] Repo created on GitHub → push scaffold (blocked: manual repo creation)
- [ ] Emotional Color Map implemented (Saraswati)
- [ ] STT input (Whisper or local)
- [ ] SVG glyph renderer
- [ ] Torsion-field spacing (`w~=`)
- [ ] Parler TTS voice output

## Station assignments

| Station | Role | Status |
|---|---|---|
| Artemis | Repo scaffold, dependency marking, coordination | ✅ done |
| Fantasia | gradient-codec upload (upstream dependency) | ✅ done — `8a69c56` |
| Saraswati | Code the map (Vector13D → CSS/SVG properties) | ⏳ next |
