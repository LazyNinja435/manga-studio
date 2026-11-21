---
name: new-manga
description: Initialize the current cloned Manga Studio repository for one manga—creating manga/ directories, manifest, series bible, creative huddle workspace, and initial art direction
---

> Convenience shortcut: Saying *"Initialize this repo for a new manga about..."* in a cloned Manga Studio repository triggers this same Director workflow.

Execute the **Single-Manga Clone Initialization** workflow as the **Manga Director** (`AGENTS.md`) using the concept or details provided in `$ARGUMENTS`:

1. **Confirm Clone Guard & Single-Manga Scope**:
   - Manga Studio is a reusable template repository; each manga lives in its own cloned Git repository under `manga/`.
   - If `manga/manga-manifest.yaml` already exists, do **not** overwrite it—report the existing manga configuration and ask whether the user wants to update it instead.
   - If this appears to be the master `manga-studio` template repository rather than a new manga clone, confirm explicitly with the user before creating `manga/`.
   - Never embed manga-specific plot or character content into template-owned files (`AGENTS.md`, `.cursor/`, `templates/`, `docs/`) so upstream template updates remain cleanly mergeable.
2. **Create Single-Manga Directory Structure Under `manga/`**:
   - `manga/creative/ideas/` (plus `manga/creative/decisions.yaml` from workspace-root `templates/creative-decision-log.yaml`; do **not** leave an active huddle session unless the user explicitly invokes `/huddle`).
   - `manga/lore/`, `manga/arcs/`, `manga/characters/`, `manga/chapters/`.
   - `manga/art/{concepts,references,panels,covers}/` and `manga/art/asset-log.yaml` (from `templates/asset-log.yaml`).
   - `manga/production/reviews/`, `manga/production/production-tracker.yaml` (from `templates/production-tracker.yaml`), and `manga/production/chronology.md` + `decisions.md` (from `templates/chronology-and-decisions.md`).
   - `manga/exports/{color,monochrome}/`.
3. **Coordinate Foundational Specialists & Skills**:
   - **`story-architect`** (skill: `series-bible`) -> Draft `manga/manga-manifest.yaml` (from `templates/manga-manifest.yaml`) and `manga/series-bible.md` (from `templates/series-bible.md`), configuring `reading_direction` (`rtl` default or `ltr`), `edition_mode` (`dual`, `color`, or `monochrome`), `page_preset` (`JIS-B5` default), and `canon_policy`.
   - **`lore-researcher`** (skill: `canon-research`) -> *Run in parallel if mythological, historical, or source-based* to establish baseline provenance and source hierarchy in `manga/lore/`.
   - **`art-director`** (skills: `visual-style-guide`, `color-and-monochrome`) -> Draft initial visual identity rules in `manga/art/art-direction.md` once premise and tone are clear.
   - Do **not** generate images during initialization unless the user explicitly asks for concept/reference art right now.
4. **Quality Gate & User Approval**:
   - Run **`manga-editor`** (skill: `editorial-review`) on `manga/series-bible.md` for hook, stakes, and thematic clarity.
   - Present the initialized manifest, series bible summary, and suggested next options (such as `/huddle` for writers'-room brainstorming, character profiling, or `/plan-arc`) as `ready-for-approval`.
