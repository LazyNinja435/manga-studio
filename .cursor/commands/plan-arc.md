---
name: plan-arc
description: Plan or revise a serialized manga story arc with chapter beats, character turns, canon verification, and editorial review
---

> Convenience shortcut: Asking *"Plan the first story arc"* in plain natural language runs this same Director workflow.

Execute the **Story Arc Planning** workflow as the **Manga Director** (`AGENTS.md`) for `$ARGUMENTS`:

1. **Verify initialized manga & baselines**:
   - Confirm `manga/manga-manifest.yaml` exists and read `manga/series-bible.md`, `manga/creative/decisions.yaml` (if present), existing `manga/characters/*.md`, `manga/lore/*.md`, and `manga/production/chronology.md`.
2. **Delegate planning & research**:
   - **`lore-researcher`** (skill: `canon-research`) -> If the manga is canon-bound or historical and source beats for this arc aren't yet documented, compile or verify `manga/lore/` baseline milestones first (or in parallel with preliminary scoping).
   - **`story-architect`** (skill: `story-arc-planning`) -> Author `manga/arcs/arc-XX-<arc-slug>.md` from workspace-root `templates/story-arc.md`, mapping setup, escalation, midpoint reversal, climax, chapter-by-chapter hooks, character transformations, and foreshadowing setups/payoffs.
3. **Independent quality gates (parallel)**:
   - **`continuity-editor`** (skill: `continuity-audit`) -> Verify chronology, character states, world rules, approved Huddle decisions, and canon alignment.
   - **`manga-editor`** (skill: `editorial-review`) -> Critique stakes, pacing rhythm, emotional payoff, and chapter-hook strength.
4. **Reconcile & present**:
   - Address `CRITICAL`/`MAJOR` review notes, log status in `manga/production/production-tracker.yaml`, and present the arc blueprint for user approval before chapter scripting begins.
