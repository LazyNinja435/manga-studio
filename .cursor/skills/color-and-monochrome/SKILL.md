---
name: color-and-monochrome
description: Design and translate manga visual storytelling across authentic full-color and traditional monochrome ink-and-screentone editions without naive grayscale conversion. Use when defining art direction, preparing edition-specific prompts, or reviewing dual-edition pages.
---

# Color and Monochrome Edition Craft

## Purpose

Ensure Manga Studio supports both **Full-Color** and **Traditional Japanese Monochrome** editions as first-class artistic mediums—sharing identical story, layout, camera, and character identity while applying authentic medium-specific craft.

## Inputs

- `manga/manga-manifest.yaml` (`edition_mode`: `color`, `monochrome`, or `dual`).
- `manga/art/art-direction.md`, `manga/characters/*.md`, and `manga/chapters/ch-XX/storyboard.md`.
- Reference matrix: [references/edition-treatment-matrix.md](references/edition-treatment-matrix.md).

## Procedure

1. **Keep Shared Structural Invariants Identical**:
   - Both editions must use the exact same script beats, panel grid, reading direction (`rtl` or `ltr`), camera angle, character poses, expressions, props, and balloon placement zones.
2. **Apply Full-Color Edition Principles**:
   - Group values first so focal characters separate cleanly from backgrounds even at thumbnail size.
   - Use controlled color keys per scene (warm amber hearth, cold slate rain, desaturated flashback, high-contrast crimson clash) rather than rainbow-saturating every surface.
   - Maintain consistent local character swatches from approved color reference sheets, modulated coherently by scene lighting.
3. **Apply Traditional Monochrome Edition Principles** (see [references/edition-treatment-matrix.md](references/edition-treatment-matrix.md)):
   - **Never convert color art to grayscale**: Desaturated color turns mid-toned hues into muddy uniform gray and destroys manga readability.
   - **Line-weight hierarchy**: Heavier, tapered G-pen contours on foreground subjects; finer Maru-pen lines on facial features, cloth folds, and distant architecture.
   - **Spotting blacks (*Beta*)**: Place deliberate solid black masses (dark hair with crisp white sheen highlights, cast shadows, cloaks, night skies) to anchor eye flow.
   - **Screentone & hatching economy**: Restrict screentones to 2–3 disciplined density tiers plus crisp crosshatching and pure white paper negative space so contrast stays razor-sharp.
4. **Maintain Separate Asset Trees**:
   - Store color assets under `art/.../color/` and `exports/color/`; store monochrome assets under `art/.../monochrome/` and `exports/monochrome/`.

## Output

- Dual-edition specifications in `art/art-direction.md`, character sheets, or `art/asset-log.yaml` prompt pairs.

## Validation

- [ ] Monochrome specifications rely on ink line weight, solid blacks, hatching, screentones, and white space—zero grayscale-filter shortcuts.
- [ ] Focal silhouettes read clearly within 1 second in both editions.
- [ ] Color and monochrome directory paths and export manifests remain cleanly separated.

## Failure Handling

- **Muddy mid-tone crowding in monochrome**: Strip mid-gray tones back to pure white negative space + solid black accents so foreground characters pop from detailed backgrounds.
- **Single-edition project later expanded to `dual`**: Reuse existing approved `script.md`, `storyboard.md`, and `lettering.md` unchanged while commissioning edition-native reference sheets and panel renders for the second edition.
