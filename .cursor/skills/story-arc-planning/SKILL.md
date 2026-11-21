---
name: story-arc-planning
description: Structure multi-chapter manga story arcs with escalating dramatic turns, serialization chapter hooks, character transformation beats, foreshadowing setups/payoffs, climax, and aftermath. Use when planning a new arc, outlining chapter sequences, or restructuring arc pacing.
---

# Story Arc Planning

## Purpose

Design serialized manga story arcs (`manga/arcs/arc-XX-<slug>.md`) that balance long-term thematic architecture with chapter-by-chapter page-turn momentum.

## Inputs

- `manga/manga-manifest.yaml`, `manga/series-bible.md`, and `manga/creative/decisions.yaml` (if present).
- Relevant character bibles (`manga/characters/*.md`), canon dossiers (`manga/lore/*.md`), and `manga/production/chronology.md`.
- Workspace-root template: `templates/story-arc.md`.

## Procedure

1. **Define the Arc Spine**:
   - State the arc's inciting disruption, central dramatic question, antagonistic force, and irreversible end-state change.
2. **Align Character & Theme**:
   - Map how external plot pressure forces the protagonist and key cast members to confront internal flaws or competing loyalties.
3. **Structure Serialization Phases** (adaptable to Kishōtenketsu or 4-part serialized manga rhythm):
   - **Setup / Hook (*Ki*)**: Ground stakes quickly; end the opening chapter with an undeniable hook.
   - **Development & Escalation (*Shō*)**: Deepen relationships, test abilities/strategies, raise complications.
   - **Twist / Reversal (*Ten*)**: Midpoint or pre-climax revelation/defeat that invalidates the protagonist's initial plan.
   - **Climax & Resolution (*Ketsu*)**: Emotional and physical confrontation, thematic choice, aftermath, and seed for the next arc.
4. **Build the Chapter-by-Chapter Beat Map**:
   - Assign each planned chapter a primary dramatic function, estimated page budget, key emotional beat, and chapter-ending page-turn hook.
5. **Log Foreshadowing Ledger**:
   - Record planted visual/dialogue clues alongside the target chapter/arc where each pays off.

## Output

- `manga/arcs/arc-XX-<arc-slug>.md`

## Validation

- [ ] Every planned chapter has a distinct dramatic shift and a clear ending hook.
- [ ] Climax resolves the arc's core conflict through character agency within established world/power limits.
- [ ] Canon-bound events align with `lore/` dossiers (or adaptations are explicitly flagged).
- [ ] Foreshadowing setups have concrete planned payoffs.

## Failure Handling

- **Missing `series-bible.md`**: Invoke or recommend `series-bible` first, or draft a lightweight provisional premise note and mark the arc `draft` pending bible lock.
- **Canon conflict discovered mid-outline**: Preserve both a canon-strict option and an adapted option in `Unresolved Questions` for `lore-researcher` and user arbitration.
- **Approved arc modification requested**: Write a `-v2` draft or clearly marked proposal section rather than silently overwriting an `approved` arc file.
