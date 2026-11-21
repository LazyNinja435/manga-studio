---
name: manga-storyboarding
description: Design manga storyboards ("name") specifying RTL or LTR panel grid layouts, eye-flow paths, camera angles, 180-degree spatial staging, action choreography, splash/spread mechanics, and balloon dead-space zones. Use when translating chapter scripts into visual page layouts.
---

# Manga Storyboarding

## Purpose

Convert `chapters/ch-XX/script.md` into a rigorous visual page-and-panel blueprint (`chapters/ch-XX/storyboard.md`) that guides the reader's eye effortlessly in the configured reading direction while staging clear camera work and reserving lettering space.

## Inputs

- `manga/manga-manifest.yaml` (`reading_direction`: `rtl` or `ltr`; `page_preset`).
- `manga/chapters/ch-XX/script.md`.
- `manga/characters/*.md` and `manga/art/art-direction.md`.
- Workspace-root template: `templates/storyboard-chapter.md`.
- Reference guide: [references/panel-flow-and-camera.md](references/panel-flow-and-camera.md).

## Procedure

1. **Lock Reading-Direction Traversal**:
   - **`rtl` (Traditional Japanese)**: Enter each page at **top-right**, scan right-to-left across each horizontal tier, descend top-to-bottom; across facing spreads, read the **right page (odd/verso in RTL book layout) before the left page**.
   - **`ltr` (Left-to-Right)**: Enter at **top-left**, scan left-to-right across tiers, descend top-to-bottom; read **left page before right page**.
2. **Design Page Hierarchy & Panel Geometry**:
   - Assign one dominant **anchor panel** per page (largest area or strongest contrast) so the page reads as a cohesive design, not a uniform checkerboard.
   - Use clean orthogonal gutters for grounded scenes; reserve angled/slanted gutters, broken borders, or full-bleed panels for kinetic spikes or psychological shock.
3. **Stage Camera & Spatial Continuity** (see [references/panel-flow-and-camera.md](references/panel-flow-and-camera.md)):
   - Vary shot scale (ELS -> MS -> CU -> ECU) and vertical angle across consecutive panels.
   - Maintain the 180-degree line of action during conversations and duels so characters don't flip screen sides disorientingly.
   - Align motion vectors **with** the reading direction (`right -> left` in RTL) for effortless speed/pursuit, and **against** the reading direction (`left -> right` in RTL) for collision, resistance, or sudden halt.
4. **Reserve Balloon & SFX Dead Space**:
   - Designate explicit upper/corner negative-space zones inside each dialogue panel so `illustration-artist` composes faces, hands, and weapons clear of text.
5. **Check Spread Spine Safety**:
   - On double-page spreads, keep faces, eyes, focal clashes, and speech balloons out of the central binding gutter (`>= 15–20 mm` safe zone around center fold).

## Output

- `manga/chapters/ch-XX/storyboard.md`

## Validation

- [ ] Panel numbering follows `reading_direction` unambiguously with zero ambiguous T-junctions or eye traps.
- [ ] No three consecutive panels repeat identical shot size and camera angle unless doing a deliberate rhythmic beat.
- [ ] Every panel containing dialogue or SFX specifies a reserved balloon/text zone.
- [ ] Double-page spreads verify facing-page parity and spine-gutter safety.

## Failure Handling

- **Overcrowded script page (> 7 panels or heavy dialogue)**: Propose a 2-page decompression split in `Unresolved Questions` rather than forcing cramped micro-panels.
- **Ambiguous action geography in script**: Define a clean spatial map at the top of the scene in `storyboard.md` so `illustration-artist` and `continuity-editor` share exact positions.
