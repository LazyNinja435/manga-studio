---
name: character-reference-art
description: Specify and produce canonical character reference sheets—orthographic turnarounds, facial expression matrices, costume/armor callouts, and weapon/prop sheets—across color and monochrome editions. Use when establishing or locking a character's visual identity.
---

# Character Reference Art

## Purpose

Bridge written character bibles (`characters/char-<slug>.md`) and locked visual model sheets (`art/references/`) so a character looks unmistakably identical from every angle, expression, and edition throughout the series.

## Inputs

- `manga/characters/char-<slug>.md` and `manga/art/art-direction.md`.
- Existing cast reference sheets in `manga/art/references/` (to preserve scale and cast contrast).
- `manga/art/asset-log.yaml`.

## Procedure

1. **Compile the Model-Sheet Specification** (`character-architect` + `art-director`):
   - **Full-Body Turnaround**: Neutral standing front, 3/4 front, side profile, and back view against a clean neutral white/light ground—no dramatic perspective distortion or heavy shadow obscuring costume seams.
   - **Expression Matrix**: Neutral baseline, determined/focused, joy/warmth, anger/combat intensity, grief/shock, and character-specific signature expression.
   - **Costume & Prop Callouts**: Layer breakdown, fastening/drape logic, scars/tattoos/jewelry exact side (`left` vs. `right`), and weapon dimensions relative to body height.
2. **Prepare Edition-Specific Sheet Prompts** (`illustration-artist`):
   - Draft dedicated **Full-Color Reference Sheet** prompt (flat/clean studio lighting, true local colors without colored mood casts) and/or **Monochrome Reference Sheet** prompt (clean black ink linework, clear solid-black hair/garment blocks, standardized screentone mapping).
3. **Generate & Verify Candidate Sheets** (when artwork is requested):
   - Place initial generations in `manga/art/concepts/char-<slug>-ref-v1.{png,webp}` and verify files exist on disk.
   - Inspect against `char-<slug>.md` invariants (handedness, scar side, outfit layers).
4. **Promote Only After User Approval**:
   - Present candidate sheet(s) as `ready-for-approval`. Once approved by the user, promote/copy to `manga/art/references/` and mark `status: approved` in `manga/art/asset-log.yaml`.

## Output

- Written turnaround/sheet spec section in `characters/char-<slug>.md` or `art/art-direction.md`.
- When image generation is invoked: candidate sheet(s) in `art/concepts/` -> promoted to `art/references/` upon user approval, logged in `art/asset-log.yaml`.

## Validation

- [ ] Reference lighting is clean and neutral (no colored sunset/neon casts distorting base swatches).
- [ ] Left/right asymmetric details (scars, sheaths, hair parts, armor pauldrons) match `char-<slug>.md`.
- [ ] Zero text/speech balloons clutter the character model turnaround.
- [ ] New visual identities remain in `concepts/` / `ready-for-approval` until the user approves them.

## Failure Handling

- **Generated turnaround drifts from character bible**: Log candidate revision (`-v2`) with tightened geometric descriptors; never silently alter the character bible to excuse an off-model image.
- **Native image tool unavailable**: Save the complete turnaround specification and edition-ready prompts so assets can be generated in a supported session without losing design work.
