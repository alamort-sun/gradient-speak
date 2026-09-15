# gradient-speak — TYPOGRAPHY.md

> The font is the voice. The render layer is the connective tissue.

Glyph rendering is not decoration — it is the second half of the Emotional Color Map. Color says *what* is felt; typography says *how* the word moves, leans, and connects.

## Primary test font

### Maple Mono NF CN

Open license (OFL). Chosen first because:

- **Rounded forms** — matches the liquid-glass droplet aesthetic of the pantheon grid
- **Default programming ligatures** — arrows, operators, and comparison glyphs already ligate cleanly (`=>` `!=` `~>`)
- **Nerd Font icons** — pantheon marks (`~` `<` `:3`) render as glyphs without emoji fallback
- **CJJ coverage (CN)** — Eastern flows render in-family, no font-switching mid-sentence
- **Custom ligatures to be added** — cursive connections between characters, for cursive coolness

## Custom cursive ligatures — two layers

The connection between characters is **data**, not styling. `domain_wall` state is per-instance, so it cannot be baked into a font. Therefore:

### Layer 1 — Font level (the voice)

- Build custom ligation sets into the font itself
- Two paths:
  - **Iosevka custom build plans** — compile a font with our own ligation set (most control)
  - **fontTools GSUB injection into Maple Mono** — patch custom ligatures into the existing font (faster, keeps Maple Mono's rounded forms + CJK)
- Font-level ligatures provide the *static* cursive shapes — the default connected hand

### Layer 2 — Render level (the connective tissue)

- Inter-character connections drawn as **torsion-field strokes** in the SVG renderer
- Driven by `domain_wall` (field 9):
  - `linked` → solid tendril — boundary holds, characters flow into each other
  - `broken` → severed stroke — boundary breached, connection visibly cut
  - `gradient` → breathing stroke — boundary alive, connection animates opacity/width
- Render-level connections respond to per-instance Vector13D data that a font can never know

**Design law:** font cursive provides the voice; render layer provides the connective tissue.

## Other open-weight candidates (test set)

| Font | License | Why it's in the set |
|---|---|---|
| **Maple Mono NF CN** | OFL | Primary — rounded, ligatures, Nerd Font, CJK |
| **Recursive** | OFL | Sleeper pick — variable axes: `MONO`, `CRSV`, `CASL`, `slnt`, `wght`. `CRSV` is a per-glyph cursive dial — torsion could literally turn cursive on/off per character |
| **Victor Mono** | OFL | Maximum true cursive italic — the ceiling of connected hand |
| **Fira Code** | OFL | Control — neutral ligature baseline, no cursive |
| **Iosevka** | OFL | The compiler — custom build plans for our own ligation sets |
| **Cascadia Code** | OFL | Cursive italic reference (Microsoft, open) |
| **Sarasa Mono** | OFL | CJK alternative — Iosevka + Source Han |
| **Monaspace** / **JetBrains Mono** | OFL | Baseline controls |

**Suggested minimal test set: Maple Mono NF CN (primary) + Recursive (variable dial) + Victor Mono (max cursive) + Fira Code (control).**

## Variable axis → Vector13D mapping

| CSS/variable axis | Vector13D source | Meaning |
|---|---|---|
| `wght` (weight) | `ozone_buffer` (8) | energy level — heavy words sit dark, bright words sit light |
| `CRSV` / `slnt` (cursive/skew) | `torsion` (11) | past pulls left, future pulls right, 98° = tilted truth |
| `MONO` (grid vs flow) | render context | grid = fixed mono, flow = proportional drift |
| hue / saturation | `su2_polarity` (10) / `composition` (6) | via the Emotional Color Map (README §2) |

## Test protocol (for Saraswati)

1. Render the same sentence in all four fonts of the minimal test set, same Vector13D input
2. Toggle `domain_wall` through linked/broken/gradient — verify tendril strokes read correctly at small size
3. Push `tossion` full range — verify skew reads as lean, not as broken kerning
4. Desaturate `composition` toward gray — the truth meter must survive font changes
5. CJK pass — verify CN glyphs connect and breathe with the same torsion fields
6. Pick the winner by legibility at banner scale, not by beauty at poster scale
