---
name: create-chapter
description: Draft a complete page-by-page, panel-by-panel manga chapter script with continuity and editorial quality reviews
---

> Convenience shortcut: Asking *"Write chapter 1"* in plain natural language invokes this same Director workflow.

Execute the **Chapter Scripting** workflow as the **Manga Director** (`AGENTS.md`) for `$ARGUMENTS`:

1. **Inspect manga prerequisites**:
   - Read `manga/manga-manifest.yaml`, `manga/series-bible.md`, `manga/creative/decisions.yaml` (if present), the active `manga/arcs/arc-XX-<arc-slug>.md`, participating `manga/characters/*.md`, relevant `manga/lore/*.md`, `manga/production/chronology.md`, and the previous chapter script (if Ch. 2+).
   - If no arc beat exists yet for this chapter, invoke **`story-architect`** (skill: `story-arc-planning`) first to outline the chapter's dramatic function.
2. **Script the chapter**:
   - Delegate to **`manga-scriptwriter`** (skill: `chapter-writing`) to write `manga/chapters/ch-XX/script.md` using workspace-root `templates/chapter-script.md`—enforcing single-moment panels, balloon-scaled editable dialogue, intentional *ma* (silent emotional beats), and page-turn hooks aligned with `reading_direction`.
   - Consult **`lore-researcher`** (skill: `canon-research`) if canonical terms, rituals, weapons, or historical details require verification.
3. **Run parallel read-only reviews**:
   - **`continuity-editor`** (skill: `continuity-audit`) -> Check timeline ticks, character knowledge, injuries, outfits, weapons, approved creative decisions, and canon fidelity.
   - **`manga-editor`** (skill: `editorial-review`) -> Evaluate show-don't-tell execution, character voice, pacing, and page-turn reveals.
4. **Revise, log & hand off**:
   - Route needed fixes back to `manga-scriptwriter`, update `manga/production/production-tracker.yaml` and `manga/production/chronology.md` notes, and present the finished script ready for approval or `/produce-pages`.
