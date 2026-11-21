---
name: review-project
description: Run comprehensive continuity, canon, visual, editorial, and publication readiness audits on the current manga repository or chapter
---

> Convenience shortcut: Asking *"Review the chapter for continuity and publication readiness"* in plain natural language runs this same Director workflow.

Execute a **Comprehensive Studio Quality Audit** as the **Manga Director** (`AGENTS.md`) for `$ARGUMENTS`:

1. **Determine audit target & scope**:
   - Verify `manga/manga-manifest.yaml` exists and determine target scope (single chapter, story arc, character roster, or full publication package).
2. **Launch independent specialist reviews** (parallelize read-only audits where applicable):
   - **`continuity-editor`** (skill: `continuity-audit`) -> Chronology, character knowledge, outfit/scar/weapon continuity, injuries, approved creative decisions (`manga/creative/decisions.yaml`), and world/power rules.
   - **`manga-editor`** (skill: `editorial-review`) -> Narrative hook, pacing, emotional payoff, dialogue sharpness, and visual readability.
   - **`lore-researcher`** (skill: `canon-research`) -> *Include when `canon_policy` is canon-bound/historical* to verify provenance tags and flag unmarked source contradictions.
   - **`art-director`** (skills: `visual-style-guide`, `color-and-monochrome`) -> *Include when `manga/art/` assets exist* to audit reference-sheet fidelity and color vs. monochrome edition craft.
   - **`publishing-director`** (skill: `manga-publishing`) -> *Include when evaluating chapter/volume completion* to verify pagination, spread parity, JIS B5/print geometry, editable lettering archival, and export manifest completeness.
3. **Consolidate & prioritize**:
   - Deduplicate findings into `CRITICAL`, `MAJOR`, and `MINOR / POLISH` items, write a dated review summary under `manga/production/reviews/`, update `manga/production/production-tracker.yaml`, and propose an ordered remediation plan.
