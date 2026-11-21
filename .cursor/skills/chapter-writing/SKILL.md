---
name: chapter-writing
description: Write page-by-page and panel-by-panel manga chapter scripts with visual storytelling, economical balloon-ready dialogue, emotional beats, silent reaction pacing, SFX cues, and page-turn reveals. Use when drafting or revising manga chapters.
---

# Chapter Writing

## Purpose

Produce production-ready manga chapter scripts (`manga/chapters/ch-XX/script.md`) engineered specifically for visual sequential art rather than prose or theatrical screenplays.

## Inputs

- `manga/manga-manifest.yaml` (`reading_direction`, `page_preset`).
- `manga/series-bible.md`, `manga/creative/decisions.yaml` (if present), active `manga/arcs/arc-XX-<arc-slug>.md`, relevant `manga/characters/*.md`, `manga/lore/*.md`, and `manga/production/chronology.md`.
- Prior chapter script (`manga/chapters/ch-(XX-1)/script.md`, if Ch. 2+).
- Workspace-root template: `templates/chapter-script.md`.

## Procedure

1. **Plan Chapter Page Architecture**:
   - Confirm target page count (commonly 18–24 pages for weekly/biweekly serialization, 30–45 for monthly/opening chapters, or custom user target).
   - Map pagination parity so big reveals, splashes, and twists land immediately **after a page turn** (even pages when Page 1 opens on an odd recto/left-turn start—confirm pagination start in manifest/storyboard).
2. **Balance Panel Density & *Ma* (間 / Decompression)**:
   - Standard pages: 4–6 panels. High-speed action or quiet contemplation: 2–4 panels. Splash impact: 1 full-page panel (or 2-page spread).
   - Use silent expression/environment panels to let emotional moments breathe instead of over-explaining in text.
3. **Enforce Single-Moment Panel Discipline**:
   - Each panel freezes **one** primary action beat. Never write "Character draws sword, dashes across the room, and blocks the strike" in a single panel—split into anticipation, motion, and clash panels.
4. **Write Balloon-Scaled Dialogue**:
   - Target <= 20–25 words per speech balloon and <= 50–60 words on most pages unless staging a deliberate negotiation scene.
   - Cut any line that merely narrates what the visual action already shows.
5. **Specify Captions & SFX Cleanly**:
   - Tag `DIALOGUE`, `THOUGHT`, `CAPTION`, and `SFX` clearly in editable script blocks so `lettering-artist` can map every element directly.

## Output

- `manga/chapters/ch-XX/script.md`

## Validation

- [ ] Every panel describes a single drawable moment in time (no multi-beat compound actions).
- [ ] Dialogue lines fit manga speech balloons comfortably and match each character's voice in `characters/*.md`.
- [ ] Major reveals and chapter-ending hooks align with page-turn positions.
- [ ] Character knowledge, injuries, props, and timeline match `manga/production/chronology.md`.

## Failure Handling

- **Arc beat exceeds chapter page budget**: Recommend splitting across two chapters with a mid-point cliffhanger rather than cramming 8–10 tiny panels onto every page.
- **Missing character bible for a minor speaking role**: Include a brief inline `[Minor Cast Visual/Voice Note]` in the script header and recommend `character-architect` formalization if the character recurs.
