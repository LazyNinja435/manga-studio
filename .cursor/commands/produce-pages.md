---
name: produce-pages
description: Transform a chapter script into storyboards, edition-specific panel illustrations, editable lettering, and reviewed manga pages
---

> Convenience shortcut: Asking *"Generate pages 1–5 of chapter 1"* in plain natural language invokes this same Director workflow.

Execute the **Manga Page Production** pipeline as the **Manga Director** (`AGENTS.md`) for `$ARGUMENTS`:

1. **Confirm scope & approved references**:
   - Read `manga/manga-manifest.yaml` for `reading_direction` (`rtl` or `ltr`), `edition_mode` (`color`, `monochrome`, or `dual`), and `page_preset` (`JIS-B5` default).
   - Verify `manga/chapters/ch-XX/script.md`, `manga/art/art-direction.md`, and approved character reference sheets in `manga/art/references/` exist. If character sheets are missing or unapproved, pause or propose establishing character references first (`character-reference-art`).
2. **Sequential visual & lettering pipeline**:
   - **Step A — `storyboard-director`** (skills: `manga-storyboarding`, `page-composition`) -> Create/update `manga/chapters/ch-XX/storyboard.md` with panel grids, shot scales, camera angles, 180-degree staging, spine-safe spreads, and reserved balloon zones.
   - **Step B — `art-director`** (skills: `visual-style-guide`, `color-and-monochrome`) -> Confirm scene lighting keys, color palette swatches, and/or monochrome ink/screentone treatments.
   - **Step C — `illustration-artist`** (skills: `image-generation`, `color-and-monochrome`, `page-composition`) -> Verify native Cursor `GenerateImage` availability, pass approved `reference_image_paths`, generate balloon-safe panel/page art separately per requested edition, verify files on disk under `manga/art/panels/`, and log provenance in `manga/art/asset-log.yaml`.
   - **Step D — `lettering-artist`** (skills: `lettering`, `page-composition`) -> Create/update `manga/chapters/ch-XX/lettering.md` with deterministic reading-order numbers, diamond-shaped editable dialogue, captions, and SFX coordinates.
3. **Parallel quality gates**:
   - **`continuity-editor`** (skill: `continuity-audit`) -> Verify visual likeness, scar/costume/weapon persistence, and spatial continuity across panels.
   - **`manga-editor`** (skill: `editorial-review`) -> Verify eye-flow readability, action comprehensibility, and balloon clarity.
4. **Synthesize & report**:
   - Reconcile any defects, update `manga/production/production-tracker.yaml`, and present verified asset paths and next steps.
