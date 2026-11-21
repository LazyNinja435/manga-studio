# Agent Routing & Delegation Guide

All ordinary user requests enter through the **Manga Director** (`AGENTS.md` + `.cursor/rules/director-routing.mdc`). At the start of every turn, the Director checks whether **Creative Huddle Mode** is explicitly active (`manga/creative/huddle-session.yaml` with `status: active`, or explicit `/huddle` activation).

---

## 1. Request-to-Specialist Routing Matrix

### Creative Huddle Mode (Manual Activation Only)

| Example User Request | Primary Facilitator | Consulted Creative Specialists | Key Skills Loaded |
|---|---|---|---|
| `"/huddle"` / *"Start a creative huddle."* | `creative-lead` | Selected on topic (`plot-architect`, `character-psychologist`, `story-critic`, `lore-researcher`) | `creative-huddle`, `creative-brainstorming` |
| `"/huddle debate ..."` / *"Debate option A vs B."* | `creative-lead` | Competing lenses across `plot-architect`, `character-psychologist`, `story-critic`, `lore-researcher` *(parallel)* | `creative-debate`, `idea-evaluation` |
| `"/huddle workshop ..."` / *"That twist feels too predictable."* | `creative-lead` | 1–2 targeted specialists (e.g., `story-critic` + `plot-architect`) | `interactive-workshop`, `idea-evaluation` |
| *"I approve option 2."* / *"Lock this idea."* (inside Huddle) | `creative-lead` | — *(logs `manga/creative/decisions.yaml`; flags affected approved files without starting production)* | `creative-decision-log` |
| `"/huddle end"` / *"End the huddle."* | `creative-lead` -> returns to Director | — *(summarizes, closes session, launches zero production)* | `creative-huddle` |

### Production Studio Mode (Default When No Huddle Is Active)

| Example User Request | Primary Specialist(s) | Review / Support Specialist(s) | Key Skills Loaded |
|---|---|---|---|
| *"Initialize this clone for a new manga about..."* (`/new-manga`) | `story-architect`, `art-director` (+ `lore-researcher` if source-based) | `manga-editor` | `series-bible`, `canon-research`, `visual-style-guide` |
| *"Research the historical/mythological canon for..."* | `lore-researcher` | `continuity-editor` (if comparing to existing drafts) | `canon-research` |
| *"Plan the first story arc."* (`/plan-arc`) | `story-architect` (+ `lore-researcher` if canon-bound) | `continuity-editor` + `manga-editor` *(parallel)* | `story-arc-planning`, `continuity-audit`, `editorial-review` |
| *"Develop the protagonist's personality and powers."* | `character-architect` | `continuity-editor`, `manga-editor` | `character-development` |
| *"Create the character reference sheet."* | `character-architect` -> `art-director` -> `illustration-artist` | `continuity-editor` | `character-reference-art`, `color-and-monochrome`, `image-generation` |
| *"Establish the full-color and monochrome style guide."* | `art-director` | `continuity-editor` | `visual-style-guide`, `color-and-monochrome` |
| *"Write chapter one."* (`/create-chapter`) | `manga-scriptwriter` (`story-architect` first if unplanned; `lore-researcher` if canonical) | `continuity-editor` + `manga-editor` *(parallel)* | `chapter-writing`, `continuity-audit`, `editorial-review` |
| *"Storyboard chapter one."* | `storyboard-director` | `continuity-editor` + `manga-editor` *(parallel)* | `manga-storyboarding`, `page-composition` |
| *"Generate five manga pages."* (`/produce-pages`) | `storyboard-director` -> `art-director` -> `illustration-artist` -> `lettering-artist` | `continuity-editor` + `manga-editor` *(parallel)* | `manga-storyboarding`, `image-generation`, `lettering`, `page-composition` |
| *"Letter chapter one / fix speech balloon order."* | `lettering-artist` | `manga-editor` | `lettering`, `page-composition` |
| *"Review the chapter for continuity and quality."* (`/review-project`) | `continuity-editor` + `manga-editor` *(parallel)* (+ `lore-researcher` if canonical) | Director synthesis | `continuity-audit`, `editorial-review`, `canon-research` |
| *"Prepare the monochrome (or color) edition for export."* | `publishing-director` | `continuity-editor` (if gates incomplete) | `manga-publishing`, `page-composition`, `color-and-monochrome` |
| *"Build a multi-arc production roadmap / resolve conflict."* | `manga-director` | — *(never delegates to itself)* | `series-bible`, `editorial-review` |

---

## 2. Parallel vs. Sequential Delegation Rules

### Safe Parallel Patterns (Single Message Batch)

Launch specialists concurrently when their inputs already exist and they write to **disjoint files** (or are `readonly: true`):

- **Huddle Roundtable / Debate**: `plot-architect` (`readonly`) || `character-psychologist` (`readonly`) || `story-critic` (`readonly`) || `lore-researcher` (read-only Huddle advisory) -> synthesized by `creative-lead`.
- **Initial Research + Premise Drafting**: `lore-researcher` (`manga/lore/...`) || `story-architect` (`manga/series-bible.md` draft).
- **Ensemble Cast Profiling**: Multiple `character-architect` tasks writing distinct `manga/characters/char-<a>.md` and `manga/characters/char-<b>.md` files.
- **Dual Quality Audits**: `continuity-editor` (`readonly`) || `manga-editor` (`readonly`) inspecting the same `script.md`, `storyboard.md`, or assembled chapter.
- **Dual-Edition Art Prompts**: Separate color and monochrome `illustration-artist` runs targeting distinct `manga/art/.../color/` and `manga/art/.../monochrome/` paths after `art-direction.md` is locked.

### Mandatory Sequential Chains

1. **Character Visual Lock**: `character-architect` (bible) -> `art-director` (sheet spec & palette/ink rules) -> `illustration-artist` (candidate sheet) -> `continuity-editor` (audit) -> **User Approval**.
2. **Chapter Page Production**: `manga-scriptwriter` (`script.md`) -> `storyboard-director` (`storyboard.md`) -> `art-director` (scene lighting/ink check) -> `illustration-artist` (`manga/art/panels/`) -> `lettering-artist` (`lettering.md`) -> parallel `continuity-editor` + `manga-editor`.
3. **Final Publication**: All upstream chapter gates -> `publishing-director` (`manga/exports/`) -> **User Publication Approval**.

---

## 3. Role-Drift Prevention Matrix

| Specialist | Owns | Must Never Do Independently |
|---|---|---|
| `manga-director` | Planning, routing, conflict resolution, tracker updates | Recursively invoke `manga-director` or loop via `creative-lead`; fabricate subagent runs |
| `creative-lead` | Single-facilitator Huddle flow, `manga/creative/` session & approved decision log | Recurse to `manga-director`; auto-approve ideas; start scripting, artwork, or publishing |
| `plot-architect` | Read-only divergent plot/twist/structure ideation in Huddles | Edit files (`readonly: true`); draft chapter scripts; lock approvals |
| `character-psychologist` | Read-only emotional logic, motivation & relationship stress-testing in Huddles | Edit files (`readonly: true`); write costume/weapon specs or scripts |
| `story-critic` | Read-only constructive disagreement & weakness/cliché testing in Huddles | Edit files (`readonly: true`); rubber-stamp weak ideas without challenge |
| `story-architect` | Formal bibles, world rules, story arcs, chapter outlines | Finalize illustrations; write full panel dialogue scripts |
| `lore-researcher` | Source comparison, provenance tags, canon dossiers + Huddle Mythology/Lore Advisor | Invent citations/verses; rewrite story plots silently |
| `character-architect` | Formal character bibles, voice, costumes, weapon & ability specs | Invoke image generation; alter approved designs silently |
| `manga-scriptwriter` | Page/panel scripts, dialogue, captions, SFX cues | Mutate established character powers/canon; lock print grids |
| `storyboard-director` | Panel grids, RTL/LTR flow, camera, spreads, balloon zones | Rewrite plot/dialogue; generate final panel artwork |
| `art-director` | Style guides, palettes, monochrome ink/tones, visual locks | Invoke `GenerateImage` directly; alter story or canon |
| `illustration-artist` | Native `GenerateImage` execution, versioned art, `asset-log.yaml` | Call external image APIs; rewrite arcs/scripts; bake body dialogue |
| `continuity-editor` | Read-only timeline, knowledge, prop, canon & visual audits | Edit or overwrite any file (`readonly: true`) |
| `lettering-artist` | Editable `lettering.md`, balloon order, line shaping, SFX map | Change story meaning; bake uneditable dialogue into raw art |
| `manga-editor` | Read-only storytelling, pacing, readability & craft review | Edit or overwrite any file (`readonly: true`) |
| `publishing-director` | Edition manifests, pagination/spread parity, JIS B5/CBZ/PDF checks | Edit story, dialogue, or artwork; self-promote to `published` |

---

## 4. Standard 7-Field Specialist Handoff

Every specialist invocation returns:

1. **Result** — Concise summary of work completed or audit verdict.
2. **Files Created or Modified** — Exact paths verified on disk (`None` for read-only roles).
3. **Assumptions** — Creative or technical defaults assumed.
4. **Unresolved Questions** — Decisions escalated to the Director/Creative Lead or user.
5. **Risks** — Continuity, canon, pacing, visual, or print hazards spotted.
6. **Review Status** — `draft` | `needs-review` | `changes-requested` | `ready-for-approval`.
7. **Recommended Next Step** — Concrete downstream specialist or user sign-off gate.
