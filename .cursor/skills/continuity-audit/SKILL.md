---
name: continuity-audit
description: Audit manga story arcs, scripts, storyboards, lettering, and generated artwork for timeline accuracy, character knowledge boundaries, personality/voice consistency, outfit/injury/weapon persistence, world rules, and canon fidelity. Use before approving or publishing manga deliverables.
---

# Continuity Audit

## Purpose

Catch temporal, logical, canonical, character, prop, and visual contradictions across a manga project before drafts are promoted to `approved` or `published`—keeping long-form serialized storytelling airtight.

## Inputs

- Target deliverable(s) under audit (`manga/arcs/`, `manga/chapters/ch-XX/`, `manga/art/`).
- Manga truth baselines: `manga/manga-manifest.yaml`, `manga/series-bible.md`, `manga/creative/decisions.yaml`, `manga/lore/*.md`, `manga/characters/*.md`, `manga/art/art-direction.md`, `manga/art/references/`, and `manga/production/chronology.md`.

## Procedure

1. **Audit Timeline & Environment (`chronology.md`)**:
   - Check elapsed days/hours, time-of-day lighting progression across scenes, weather/seasons, travel distances, and character ages.
2. **Audit Epistemic State (Character Knowledge)**:
   - Verify each speaking character only acts on or mentions facts, names, alliances, or betrayals they have personally witnessed or been told on-page/in-backstory.
3. **Audit Physical, Costume & Prop State**:
   - Track left/right handedness, permanent scars/marks, active wounds/bandages, torn garments, armor pieces removed, arrows/ammunition spent, and weapon draw/sheathe state panel-by-panel.
4. **Audit World Mechanics & Power Ceilings**:
   - Confirm combat feats, magic/spiritual rules, and stamina costs obey limits locked in `series-bible.md` and `characters/*.md`.
5. **Audit Canon & Provenance Alignment** (for canon-bound projects):
   - Compare events, vows, titles, and relationships against `lore/*.md` and `canon_policy`, flagging any unmarked departures.
6. **Audit Visual & Spatial Continuity** (for storyboards & images):
   - Check 180-degree axis consistency, character height ratios, model-sheet likeness, and left/right prop placement across consecutive panels.
7. **Classify & Cite Findings**:
   - Rank every issue (`CRITICAL`, `MAJOR`, `MINOR`), cite both the offending page/panel and the exact baseline truth section, and propose the smallest clean fix without editing files directly.

## Output

- Structured Continuity Audit Report returned to the Director (and logged by the Director in `manga/production/reviews/` + `manga/production/chronology.md` updates).

## Validation

- [ ] Every flagged contradiction cites both target location and baseline source file.
- [ ] Audit covers chronology, character knowledge, physical/prop state, world rules, canon alignment, and visual continuity.
- [ ] Zero project files were modified directly during the read-only audit.

## Failure Handling

- **`chronology.md` missing or outdated**: Reconstruct baseline state from earlier approved chapters/arcs, note the gap explicitly, and provide exact ledger entries for the Director to write into `manga/production/chronology.md`.
- **Ambiguous intentional retcon vs. accidental error**: Flag as `Unresolved Question` requiring Director/user confirmation rather than assuming error or intent.
