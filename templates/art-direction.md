---
artifact_type: art-direction
manga_slug: "<manga-slug>"
edition_mode: "dual" # color | monochrome | dual
version: "0.1"
status: "draft" # draft | ready-for-approval | approved
---

# Master Art Direction — `<Manga Title>`

## 1. Visual Identity & Proportions

- **Aesthetic Pillar**: <Core visual character, era flavor, and emotional atmosphere>
- **Anatomical & Proportion Standard**: <Head-to-body ratios, facial stylization level, silhouette contrast rules>
- **Linework Language**:
  - *Foreground Contours*: <e.g., expressive tapered G-pen weight>
  - *Interior Anatomy & Drapery*: <e.g., crisp fine Maru-pen folds>
  - *Action & Impact Effects*: <Speedlines, brush streaks, impact flashes>

## 2. Full-Color Edition Specification

- **Master Value & Saturation Rules**: <Value grouping priority, saturation restraint vs. focal accents>
- **Scene Color Keys / Lighting Scripts**:
  - *Daylight Exterior*: <Key/fill/sky palette>
  - *Nocturnal / Torchlight*: <Ambient shadow hue + warm key falloff>
  - *High-Drama / Climax*: <Contrast & rim-light shift>
- **Shading & Texture**: <Cel-shaded / two-tone / painterly blend rules>

## 3. Traditional Monochrome Edition Specification

> Monochrome art is crafted natively in black ink, hatching, screentones, and pure white negative space—**never** converted from color via grayscale desaturation.

- **Solid Black (*Beta*) Spotting**: <Hair blocks, cast shadows, garment anchors, sheen highlights (*tsuya beta*)>
- **Screentone Hierarchy**:
  - *Light Tone (~10–15%)*: <Subtle fabric/ambient differentiation>
  - *Mid Tone (~30–40%)*: <Secondary clothing, twilight sky, stone>
  - *Deep Tone (~60%+)*: <Heavy shadow mood, nocturnal backdrops>
- **Crosshatching & Negative Space**: <Where hand hatching replaces tone; white halo (*nuki*) rules around overlapping silhouettes>

## 4. Approved Character Reference Registry

| Character Slug | Color Ref Path | Monochrome Ref Path | Approval State |
|---|---|---|---|
| `<char-slug>` | `art/references/color/char-<slug>-ref.png` | `art/references/monochrome/char-<slug>-ref.png` | `pending` |

## 5. Environment & Architecture References

- **Recurring Locations**: <Key settings, architectural motifs, foliage/weather styling, background drop-out rules>

## 6. Prompt Vocabulary & Anti-Drift Guardrails

- **Canonical Style Descriptors**: `<reusable positive descriptors for illustration-artist>`
- **Forbidden Drift Elements**: `no embedded speech bubbles, no dialogue text, no 3D CGI plastic sheen, no grayscale-filtered muddy midtones`
