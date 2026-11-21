---
name: page-composition
description: Apply Japanese B5 and configurable manga page geometry—trim, bleed, live safe area, spine gutter allowances, splash framing, and double-page spread alignment—across storyboarding, illustration, lettering, and publishing. Use when composing pages, spreads, or print-ready layouts.
---

# Page Composition & Print Geometry

## Purpose

Ensure every manga page, single-page splash, and double-page spread adheres to professional manga page proportions and print-safe margins (centered on standard **JIS B5** with support for configurable presets) so critical art and dialogue are never clipped at trim or swallowed in the book spine.

## Inputs

- `manga/manga-manifest.yaml` (`page_preset`, `reading_direction`, custom dimensions if specified).
- `manga/chapters/ch-XX/storyboard.md`, `lettering.md`, and `manga/art/` specifications.
- Reference spec: [references/b5-print-specs.md](references/b5-print-specs.md).

## Procedure

1. **Confirm Active Page Preset** (see [references/b5-print-specs.md](references/b5-print-specs.md)):
   - Default to **JIS B5 Manga Tankōbon / Magazine Preset** (`182 × 257 mm` trim, `3 mm` bleed on all outer edges -> `188 × 263 mm` full canvas; `150 × 220 mm` inner live/safe frame) unless `manga/manga-manifest.yaml` specifies Tankōbon B6, A5, or US Trade.
2. **Respect the Three Concentric Page Zones**:
   - **Bleed Edge**: Background sky, explosions, and full-bleed splash borders must extend all the way to the outer bleed boundary so trimming leaves no white slivers.
   - **Trim Line**: Actual finished page edge (`182 × 257 mm` for B5). Never place faces, fingers, or panel corners unintentionally tangent to trim.
   - **Safe / Live Area (`uchi-waku`)**: Keep all standard panel borders, speech balloons, captions, page numbers, and essential facial expressions strictly inside the inner safe margin.
3. **Account for Binding Spine Side (`nodomoto`)**:
   - Add extra inner-margin clearance on the binding edge (`>= 18–22 mm` from trim toward center spine) because perfect-bound tankōbon volumes curve into the glue gutter.
   - Note that binding side alternates between odd and even pages according to `reading_direction` (`rtl` binds on the **right** side of the closed book; `ltr` binds on the **left**).
4. **Engineer Double-Page Spreads Safely**:
   - Confirm the two pages form a true facing pair (even + odd in `ltr`; odd-right + even-left in `rtl` depending on page-1 start convention—verify in manifest/export map).
   - Keep a `30–40 mm` combined center-fold caution zone (`15–20 mm` each side of spine) free of faces, eyes, weapon contact points, and single balloons spanning the fold.

## Output

- Page geometry metadata and safe-zone constraints applied in `storyboard.md`, `lettering.md`, `art-direction.md`, and `exports/`.

## Validation

- [ ] All speech balloons, captions, and critical facial expressions sit inside the live safe area.
- [ ] Full-bleed splashes extend background imagery cleanly through the 3 mm bleed margin.
- [ ] Double-page spreads land on facing pages and keep focal faces/text clear of the center spine fold.

## Failure Handling

- **Native image tool aspect ratio differs slightly from exact JIS B5 (`~1:1.412`)**: Use `3:4` (`1:1.333`) for vertical pages and compose with generous outer bleed/safe buffer at left/right edges so trimming/fitting to B5 (`182 × 257 mm`) preserves the entire inner safe zone intact.
- **Spread lands on non-facing odd/even pages after script edit**: Flag pagination parity mismatch immediately so `manga-scriptwriter` or `publishing-director` adjusts lead-in page count or single-page pacing before page production.
