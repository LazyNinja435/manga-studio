---
name: manga-publishing
description: Organize completed manga chapters and volumes into publication-ready full-color and monochrome edition packages—verifying pagination, spread parity, B5/print bleed and margin geometry, deterministic file naming, editable text preservation, and PDF/CBZ export readiness. Use when preparing chapters or volumes for export or publication.
---

# Manga Publishing

## Purpose

Verify and package completed manga chapters or collected volumes into clean, separated **Full-Color** and **Monochrome** publication deliverables (`manga/exports/`) ready for digital readers (CBZ/PDF) and print-ready workflows (JIS B5 and custom presets).

## Inputs

- `manga/manga-manifest.yaml`.
- Approved chapter sources: `manga/chapters/ch-XX/{script.md,storyboard.md,lettering.md}`.
- Verified artwork in `manga/art/panels/{color,monochrome}/`, `manga/art/covers/`, and `manga/art/asset-log.yaml`.
- Quality gate records in `manga/production/production-tracker.yaml` and `manga/production/reviews/`.
- Workspace-root template: `templates/export-manifest.md`.

## Procedure

1. **Audit Upstream Quality Gates**:
   - Confirm story, canon (where applicable), continuity, visual consistency, lettering, and editorial gates are marked passed/approved in `production-tracker.yaml`. Flag any missing or failed gates before packaging.
2. **Verify Pagination Sequence & Spread Parity**:
   - Build an explicit page index from front cover / inside title lead through final chapter page and back matter.
   - Confirm every double-page spread lands on true facing verso/recto pages in the project's `reading_direction` (`rtl` vs. `ltr`). Insert an intentional title/credit/illustration lead page if needed to fix odd/even parity so a spread never splits across a page turn.
3. **Validate Edition Separation & Asset Integrity**:
   - Confirm every page image listed in `exports/color/` and/or `exports/monochrome/` exists on disk and matches its target edition (`monochrome` uses dedicated black-and-white ink/tone assets, never desaturated color files).
   - Confirm editable source text (`script.md` and `lettering.md`) is archived alongside the package for future reprints or translation.
4. **Verify Print & Archive Specifications**:
   - **Print readiness**: Check page aspect ratio, `JIS-B5` (`182 × 257 mm` trim + `3 mm` bleed = `188 × 263 mm`) or custom preset compliance, safe inner spine margin clearance, and resolution/color-mode notes (sRGB for digital; CMYK / 600-DPI 1-bit or grayscale guidance for offset/POD print).
   - **CBZ / PDF readiness**: Define zero-padded sequential filenames (`000-cover.png`, `001.png`, `002.png`, ...; spreads named `004-005-spread.png` or split per reader target) plus standard `ComicInfo.xml` / metadata fields (`Manga="YesAndRightToLeft"` for `rtl` CBZ readers).
5. **Write Export Manifest & Hold for Final User Sign-Off**:
   - Write `manga/exports/{color,monochrome}/ch-XX-export-manifest.md` and set package status to `ready-for-approval` until the user explicitly authorizes `published`.

## Output

- `manga/exports/color/ch-XX-export-manifest.md` (when `color` or `dual`)
- `manga/exports/monochrome/ch-XX-export-manifest.md` (when `monochrome` or `dual`)
- Updated readiness records in `manga/production/production-tracker.yaml`

## Validation

- [ ] All upstream review gates are verified and cited.
- [ ] Every referenced image and editable lettering file exists on disk.
- [ ] Double-page spreads align on facing pages under `reading_direction`.
- [ ] Color and monochrome edition manifests are strictly separated.
- [ ] No story, dialogue, or artwork files were altered during packaging.

## Failure Handling

- **Missing page artwork or unapproved reference asset**: Halt publication sign-off, mark the export checklist `blocked` with an exact missing-asset inventory, and route back to `illustration-artist` / `art-director` via the Director.
- **Spread parity broken**: Propose concrete pagination insertion options (inside title plate, chapter illustration page, or cast frontispiece) for Director/user approval rather than splitting a spread across non-facing pages.
