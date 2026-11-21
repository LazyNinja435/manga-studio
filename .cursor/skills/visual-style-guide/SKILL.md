---
name: visual-style-guide
description: Define a manga project's master visual style guide covering linework character, proportion rules, lighting language, architectural/environment aesthetics, full-color palette systems, and monochrome ink/screentone standards. Use when establishing or updating art direction for a project.
---

# Visual Style Guide

## Purpose

Create `manga/art/art-direction.md` so every character sheet, environment concept, panel illustration, and cover shares one cohesive visual DNA across full-color and monochrome editions.

## Inputs

- `manga/manga-manifest.yaml` (`genre`, `target_audience`, `edition_mode`, `page_preset`).
- `manga/series-bible.md`, `manga/lore/*.md` (period/material culture notes), and initial `manga/characters/*.md`.
- Workspace-root template: `templates/art-direction.md`.

## Procedure

1. **Define Overall Aesthetic & Proportion Rules**:
   - Specify head-to-body ratio norms by age/build, facial stylization vs. anatomical realism balance, and silhouette readability standards.
2. **Specify Ink & Linework Vocabulary**:
   - Define outer contour weight, interior anatomical/cloth fold weight, hair/eye detail weight, and kinetic brush/speedline style (e.g., crisp G-pen taper vs. textured dry-brush energy).
3. **Establish Full-Color System**:
   - Define master saturation/value range, character signature color accents, environment mood palettes (dawn, harsh noon, torchlight, nocturnal), and cel vs. soft-gradient shading policy.
4. **Establish Traditional Monochrome System**:
   - Define solid black (*beta*) spotting ratios, screentone density tiers (light skin/fabric accents, mid-tones, deep shadow tones), crosshatching rules, and white negative-space preservation.
5. **Define Environment & Background Standards**:
   - Document recurring architectural motifs, foliage/weather rendering level, perspective rigor, and when backgrounds drop out for emotional/impact focus.
6. **Lock Prompt Vocabulary**:
   - Record canonical positive style descriptors and forbidden drift descriptors (`anti-style` tags such as photorealistic 3D render, baked speech bubbles, grayscale-washed muddiness) for `illustration-artist`.

## Output

- `manga/art/art-direction.md`

## Validation

- [ ] Both **Full-Color** and **Monochrome** sections contain specific, independent artistic directives (never "convert color to grayscale").
- [ ] Linework, proportion, lighting, and background rules align with `series-bible.md` tone and `lore/` period details.
- [ ] Canonical style keywords and anti-drift guardrails are documented for consistent prompting.

## Failure Handling

- **Conflicting tone cues (e.g., gritty realism vs. stylized comedy beats)**: Define explicit primary style plus bounded secondary shift rules (e.g., subtle reaction simplification allowed, full chibi distortion prohibited).
- **Approved art direction already exists**: Propose versioned additions rather than rewriting locked style rules without user sign-off.
