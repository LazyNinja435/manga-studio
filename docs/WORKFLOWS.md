# Studio Production & Ideation Workflows

Every workflow below runs inside a **cloned single-manga repository** (never inside the master `manga-studio` template repository) and stores all manga-specific files under `manga/`. Natural-language prompts work identically to the optional `/command` shortcuts.

---

## 0. Creative Huddle Mode (`/huddle`) — Optional Pre-Production Writers' Room

**Goal:** Brainstorm, debate, and workshop story concepts, twists, character conflicts, and canon choices conversationally before committing to formal production files.

1. Creator manually triggers `/huddle` (or *"Start a creative huddle"*).
2. **Creative Lead** initializes or resumes `manga/creative/huddle-session.yaml` (`status: active`) and opens in `roundtable`, `debate`, or `workshop` mode.
3. Creative Lead consults read-only creative specialists (`plot-architect`, `character-psychologist`, `story-critic`, and `lore-researcher` as Mythology/Lore Advisor) selectively and synthesizes options in one conversational voice.
4. Ideas move cleanly through `PROPOSED` -> `EXPLORING` -> `CANDIDATE` -> `APPROVED` (logged in `manga/creative/decisions.yaml` only on explicit creator sign-off) | `REJECTED` | `DEFERRED`.
5. Creator exits via `/huddle end` (or *"End the huddle"*): session is summarized, closed (`status: closed`), and control returns to normal **Manga Director** routing **without** auto-starting production.

*(Full details: [`docs/CREATIVE-HUDDLE.md`](CREATIVE-HUDDLE.md).)*

---

## 1. Clone Initialization & New Manga Setup (`/new-manga`)

**Goal:** Configure a freshly cloned repository for **one manga**—scaffolding `manga/` directories, format lock, canon policy, series bible, creative decision log, and baseline art direction without prematurely writing chapters or generating artwork.

1. **Director** verifies this is a dedicated manga clone (never initializing `manga/` inside the master template repo) and creates the `manga/` directory layout (`creative/`, `lore/`, `arcs/`, `characters/`, `chapters/`, `art/`, `production/`, `exports/`).
2. **Parallel Discovery** *(when source-based)*:
   - `lore-researcher` (`canon-research`) builds initial provenance & source hierarchy notes in `manga/lore/`.
   - `story-architect` (`series-bible`) drafts `manga/manga-manifest.yaml` (`reading_direction`, `edition_mode`, `JIS-B5` preset, `canon_policy`) and `manga/series-bible.md`.
3. **Sequential Visual Foundation**:
   - `art-director` (`visual-style-guide`, `color-and-monochrome`) drafts `manga/art/art-direction.md` with distinct Full-Color and Monochrome rules.
4. **Editorial Gate**:
   - `manga-editor` (`editorial-review`) reviews premise hook, thematic tension, and boundaries.
5. **Director** initializes `manga/production/{production-tracker.yaml,chronology.md,decisions.md}`, `manga/creative/decisions.yaml`, and `manga/art/asset-log.yaml`, presenting the foundation as `ready-for-approval`.
6. **User Approval Gate**: Creator confirms reading direction, edition mode, canon policy, and series premise.

---

## 2. Story Arc Development (`/plan-arc`)

**Goal:** Design a serialized multi-chapter arc with clear emotional stakes, chapter hooks, and verified canon/continuity alignment.

1. **Director** reads `manga/manga-manifest.yaml`, `manga/series-bible.md`, `manga/creative/decisions.yaml`, `manga/characters/*.md`, `manga/lore/*.md`, and `manga/production/chronology.md`.
2. `lore-researcher` (`canon-research`) validates source episodes and variants if canon-bound.
3. `story-architect` (`story-arc-planning`) writes `manga/arcs/arc-XX-<arc-slug>.md` (Ki-Shō-Ten-Ketsu beats, chapter beat map, character crucibles, foreshadowing ledger).
4. **Parallel Review Gate**:
   - `continuity-editor` (`continuity-audit`) checks timeline, world rules, approved creative decisions, and canon alignment.
   - `manga-editor` (`editorial-review`) evaluates escalation, midpoint twist, and chapter-ending hooks.
5. **Director** reconciles notes and presents the arc for **User Approval**.

---

## 3. Character Development & Reference Lock

**Goal:** Create psychologically distinct characters with locked silhouettes and reference sheets before chapter illustration begins.

1. `character-architect` (`character-development`) creates `manga/characters/char-<slug>.md` (psychology, voice, relationships, physical anchors, handedness, scars, costumes, weapon specs, ability limits).
2. `art-director` (`character-reference-art`, `color-and-monochrome`) defines orthographic turnaround, expression matrix, color swatches, and monochrome ink/tone specs.
3. *(When visual sheet generation is requested)* `illustration-artist` (`image-generation`) generates candidate reference sheets into `manga/art/concepts/` using Cursor's native `GenerateImage`, verifies files on disk, and logs provenance in `manga/art/asset-log.yaml`.
4. `continuity-editor` verifies sheet accuracy against `char-<slug>.md` invariants and `manga/lore/`.
5. **User Approval Gate**: Once approved, sheets are promoted to `manga/art/references/{color,monochrome}/` and locked as canonical references.

---

## 4. Chapter Creation (`/create-chapter`)

**Goal:** Write a tight, visually driven page-by-page and panel-by-panel script (`manga/chapters/ch-XX/script.md`).

1. **Director** verifies arc context, `manga/creative/decisions.yaml`, active cast states in `manga/production/chronology.md`, and prior chapter pickup. (`story-architect` outlines beats first if no arc plan exists.)
2. `manga-scriptwriter` (`chapter-writing`) authors `manga/chapters/ch-XX/script.md`—one frozen moment per panel, concise editable dialogue (`<= 25 words/balloon`), silent *ma* reaction beats, and page-turn reveals aligned with `reading_direction`.
3. **Parallel Review Gate**:
   - `continuity-editor` audits timeline progression, epistemic knowledge, wounds, outfits, weapons, and approved decisions.
   - `manga-editor` critiques show-don't-tell, voice differentiation, and page-turn propulsion.
4. `manga-scriptwriter` resolves flagged issues; **Director** updates `manga/production/production-tracker.yaml` and `chronology.md`.

---

## 5. Native Image Production

**Goal:** Generate consistent character sheets, environments, panels, splashes, or covers using Cursor's built-in image generation without external tools.

1. `illustration-artist` (`image-generation`) checks native `GenerateImage` availability via `GetDynamicTools`.
2. Loads `manga/art/art-direction.md`, `storyboard.md` framing + balloon zones, and approved `reference_image_paths` from `manga/art/references/`.
3. Executes separate native generations for **Full-Color** (`manga/art/.../color/`) and **Monochrome** (`manga/art/.../monochrome/`)—never converting color art to grayscale and keeping body dialogue out of raw artwork.
4. Verifies every output file exists on disk and appends full provenance to `manga/art/asset-log.yaml` using versioned naming (`-v1`, `-v2`) so approved files are never overwritten.
5. `art-director` + `continuity-editor` review visual likeness and continuity.

---

## 6. Full Page Production (`/produce-pages`)

**Goal:** Take an approved `script.md` through layout, illustration, editable lettering, and page review.

1. `storyboard-director` (`manga-storyboarding`, `page-composition`) builds `manga/chapters/ch-XX/storyboard.md` with `rtl`/`ltr` panel sequence, shot variety, 180-degree staging, JIS B5 safe margins, spread spine clearance, and reserved balloon zones.
2. `art-director` locks scene lighting keys / monochrome ink-tone density.
3. `illustration-artist` generates balloon-safe panel/page art in `manga/art/panels/{color,monochrome}/` and logs `manga/art/asset-log.yaml`.
4. `lettering-artist` (`lettering`, `page-composition`) authors `manga/chapters/ch-XX/lettering.md` with deterministic balloon reading order, diamond-shaped editable lines, captions, and SFX maps.
5. **Parallel Review Gate**: `continuity-editor` + `manga-editor` audit visual continuity, action clarity, and reading flow.

---

## 7. Studio Quality Review (`/review-project`)

**Goal:** Audit any artifact, chapter, or the entire manga repository across all six quality dimensions defined in `.cursor/rules/quality-gates.mdc`.

1. **Parallel Read-Only Audits**:
   - `continuity-editor` -> Timeline, character knowledge, outfits/weapons/injuries, approved creative decisions, world rules, visual model lock.
   - `manga-editor` -> Hook, emotional stakes, pacing, dialogue sharpness, action legibility.
   - `lore-researcher` -> Provenance & source fidelity *(for canon-bound manga)*.
   - `art-director` / `lettering-artist` / `publishing-director` -> Domain checks as applicable.
2. **Director** deduplicates findings into `CRITICAL`, `MAJOR`, and `MINOR`, writes a review record to `manga/production/reviews/`, and routes targeted fixes to owning specialists.

---

## 8. Publication & Edition Packaging (Skill: `manga-publishing`)

**Goal:** Package verified **Full-Color** and/or **Monochrome** chapters or volumes for CBZ, PDF, and JIS B5/print workflows.

1. `publishing-director` (`manga-publishing`, `page-composition`) confirms all upstream quality gates in `manga/production/production-tracker.yaml` have passed.
2. Verifies page sequence and recto/verso parity so every double-page spread lands on facing pages in `rtl` or `ltr` pagination.
3. Confirms separate edition asset integrity (`manga/exports/color/` vs. `manga/exports/monochrome/`), JIS B5 (`182 × 257 mm` trim + `3 mm` bleed) safe-zone compliance, zero-padded archive naming (`001.png`, ...), `ComicInfo.xml` metadata notes, and archived editable `lettering.md`.
4. Marks export manifests `ready-for-approval` and awaits **Final User Publication Approval** before setting status to `published`.
