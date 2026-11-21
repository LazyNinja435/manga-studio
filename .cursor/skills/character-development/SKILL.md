---
name: character-development
description: Create or refine manga character bibles covering biography, psychology, motivations, speech voice, interpersonal dynamics, transformation arcs, silhouette-distinct appearance, costumes, weapons, abilities, and continuity invariants. Use when designing new characters or evolving existing cast profiles.
---

# Character Development

## Purpose

Author rich, consistent character bibles (`manga/characters/char-<slug>.md`) that equip scriptwriters with unmistakable voice and motivation while giving art teams concrete, silhouette-distinct visual anchors.

## Inputs

- Character concept, narrative role, and arc context (`manga/series-bible.md`, `manga/creative/decisions.yaml`, `manga/arcs/*.md`, `manga/lore/*.md`).
- Existing `manga/characters/*.md` files (for cast contrast check).
- Workspace-root template: `templates/character-bible.md`.

## Procedure

1. **Anchor Dramatic Identity**:
   - Define role in ensemble, conscious external goal (**Want**), unconscious emotional truth (**Need**), core flaw/fear, and moral line they will or will not cross.
2. **Establish Voice & Behavior**:
   - Specify speech cadence, formality/register, emotional tells under stress, humor/silence habits, and 2–3 brief sample lines demonstrating voice without locking plot dialogue.
3. **Map Relationships**:
   - Document concrete dynamics with other named characters (trust level, power asymmetry, shared history, point of friction).
4. **Design Silhouette-Readable Visual Anchors**:
   - Contrast height, build, hair silhouette, eye geometry, posture, and signature garment shapes against existing cast members (the "silhouette test").
   - Specify handedness, permanent marks/scars, default outfit layers, variant outfits (travel, combat, ceremonial), and signature weapons/props.
5. **Bound Abilities & Combat Style**:
   - Define fighting or skill style, tactical strengths, explicit weaknesses, stamina/resource costs, and hard ceilings.
6. **List Continuity Invariants**:
   - Summarize non-negotiable traits `continuity-editor` must check in every chapter and panel.

## Output

- `manga/characters/char-<character-slug>.md`

## Validation

- [ ] Character's silhouette, speech pattern, and flaw are clearly distinct from existing cast files.
- [ ] Physical traits include handedness, height/build reference, eye/hair shapes, and costume layer details sufficient for `art-director`.
- [ ] Abilities include explicit limitations and failure conditions.
- [ ] Canon provenance is noted if adapting a mythological or historical figure.

## Failure Handling

- **Approved character redesign requested**: Do not overwrite an `approved` character bible silently; draft a versioned revision proposal and flag user approval requirement.
- **Missing world/power rules**: Coordinate via Director with `story-architect` rather than inventing unbounded world mechanics inside a single character file.
