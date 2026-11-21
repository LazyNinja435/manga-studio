---
name: series-bible
description: Initialize or update a manga repository's manifest and series bible—defining premise, genre, audience, reading direction, dual-edition format, canon policy, worldbuilding rules, themes, and story boundaries. Use when initializing a cloned manga repository via /new-manga or formalizing foundational series rules.
---

# Series Bible

## Purpose

Establish the authoritative creative and technical constitution for a cloned manga repository (`manga/manga-manifest.yaml` and `manga/series-bible.md`) so every specialist works from shared world rules, themes, reading direction, edition format, and canonical boundaries.

## Inputs

- User concept, logline, inspiration, or genre goals.
- Workspace-root templates: `templates/manga-manifest.yaml`, `templates/series-bible.md`, `templates/production-tracker.yaml`, `templates/chronology-and-decisions.md`, `templates/creative-decision-log.yaml`, and `templates/asset-log.yaml`.
- Optional: Initial canon dossier (`manga/lore/*.md`) if adapting mythology, history, or existing IP, and approved decisions in `manga/creative/decisions.yaml`.

## Procedure

1. **Verify Clone Initialization Guard**:
   - Manga Studio is a single-manga-per-clone template repository; never initialize `manga/` inside the master template repo without explicit confirmation that this workspace is a dedicated manga clone.
   - If `manga/manga-manifest.yaml` already exists, update carefully without overwriting approved fields silently.
2. **Configure `manga/manga-manifest.yaml`** from workspace-root `templates/manga-manifest.yaml`:
   - Set `manga_slug`, `title`, `genre`, `target_audience` (e.g., shōnen, seinen, shōjo, josei, all-ages), `reading_direction` (`rtl` default for traditional manga, or `ltr`), `edition_mode` (`dual`, `color`, or `monochrome`), `page_preset` (default `JIS-B5`), `canon_policy` (`original-fiction`, `strict-canon`, `faithful-adaptation`, or `inspired-reimagining`), and `status: draft`.
3. **Draft `manga/series-bible.md`** from workspace-root `templates/series-bible.md`:
   - **High-Concept Premise**: 2–3 sentence hook, dramatic question, and core conflict.
   - **Thematic Spine**: Central thematic tension tested through action rather than preached in dialogue.
   - **World Rules & Constraints**: Geography, era/society, technology or supernatural/martial mechanics, and explicit hard limits/costs.
   - **Narrative Conventions**: Tone balance, content boundaries, POV rules, and serialization pacing target.
   - **Story Boundaries**: Non-negotiable guardrails (what never happens in this world; locked canonical endpoints if applicable).
4. **Scaffold Initial Repository Memory** (on first initialization of a manga clone):
   - Initialize `manga/production/production-tracker.yaml` from workspace-root `templates/production-tracker.yaml`.
   - Initialize `manga/production/chronology.md` and `manga/production/decisions.md` from workspace-root `templates/chronology-and-decisions.md`.
   - Initialize `manga/creative/decisions.yaml` from workspace-root `templates/creative-decision-log.yaml` and `manga/art/asset-log.yaml` from workspace-root `templates/asset-log.yaml`.
   - Do **not** create an active `huddle-session.yaml` unless the user explicitly invoked `/huddle`.
5. **Flag Approval Gate**:
   - Mark manifest and series bible `ready-for-approval` so the user locks reading direction, edition format, and canon policy before heavy downstream production.

## Output

- `manga/manga-manifest.yaml`
- `manga/series-bible.md`
- `manga/production/{production-tracker.yaml,chronology.md,decisions.md}`, `manga/creative/decisions.yaml`, and `manga/art/asset-log.yaml` (on clone initialization)

## Validation

- [ ] `reading_direction`, `edition_mode`, `page_preset`, and `canon_policy` are explicitly populated.
- [ ] World/power rules include concrete limitations and costs, not only capabilities.
- [ ] Story boundaries clearly distinguish canonical constraints from open creative space.
- [ ] Zero template-owned files (`AGENTS.md`, `.cursor/`, `templates/`, `docs/`) were polluted with manga-specific story data.

## Failure Handling

- **Master template ambiguity**: If this workspace appears to be the uncloned master `manga-studio` repository, stop and ask the user to confirm whether they meant to clone it first.
- **Underspecified premise**: Propose sensible genre-appropriate defaults clearly marked as `[Assumed — confirm]` in the handoff summary rather than stalling on minor metadata.
- **Missing source canon clarity**: Set `canon_policy` conservatively (`faithful-adaptation`) and recommend `lore-researcher` validation before locking.
