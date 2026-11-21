# Manga Studio

**Manga Studio** is a reusable, 100% Cursor-native **template repository** for creating professional manga—combining a **Production Studio** (planning, research, scripting, storyboarding, art direction, native illustration, editable lettering, continuity/editorial review, and publication packaging across **Full-Color** and **Traditional Monochrome** editions) with an AstrAI-inspired **Creative Huddle Mode** (a conversational AI writers' room for brainstorming, debate, and iterative workshopping).

There is no external orchestration server, custom CLI, database, or third-party image API to maintain. Cursor's Agent runtime **is** the studio engine—powered by `AGENTS.md`, 16 specialist subagents (12 production + 4 Creative Huddle specialists), 7 contextual rules, 21 skills, 7 slash-command shortcuts, and structured file-based memory.

---

## Template Repository Model (One Manga Per Clone)

**No manga is developed directly inside this master `manga-studio` repository.** Every manga series is created by cloning this template into its own independent Git repository:

```bash
# 1. Create a new repository from this template (or clone it)
git clone <manga-studio-repo-url> my-new-manga
cd my-new-manga

# 2. Point origin to your new manga's repository and keep the template as an upstream remote
git remote rename origin template
git remote add origin <your-new-manga-repo-url>
```

Inside your new cloned repository, open it in Cursor and run `/new-manga` (or say *"Initialize this repo for a new manga about..."*) to scaffold `manga/` for that single series.

### Clean Upstream Synchronization

Manga Studio separates **template-owned studio files** from **manga-owned story files** so you can pull studio upgrades anytime without merge conflicts:

- **Template-owned (master repo)**: `AGENTS.md`, `.cursor/agents/`, `.cursor/rules/` (studio rules), `.cursor/skills/`, `.cursor/commands/`, `templates/`, `docs/`, `README.md`.
- **Manga-owned (clone-only — never present in master template)**: Everything under `manga/`, plus optional clone-specific rules named `.cursor/rules/local-*.mdc`.

To pull future Manga Studio updates into an active manga clone:

```bash
git fetch template
git merge template/main   # Updates agents/skills/rules/docs cleanly without touching manga/
```

---

## Two Working Modes: Production Studio & Creative Huddle

### 1. Director-First Production Studio (Default)

Every ordinary natural-language prompt enters through the **Manga Director** (`AGENTS.md` + `.cursor/rules/director-routing.mdc`). You never need to invoke specialists manually:

- *"Initialize this clone for a new right-to-left dual-edition manga about..."* (`/new-manga`)
- *"Develop the protagonist's personality, costume layers, and combat limits."*
- *"Plan the opening 6-chapter arc."* (`/plan-arc`)
- *"Write chapter 1."* (`/create-chapter`)
- *"Create the character reference sheet in monochrome and color."*
- *"Generate pages 1–5 of chapter 1."* (`/produce-pages`)
- *"Review chapter 1 for continuity and pacing."* (`/review-project`)
- *"Prepare the monochrome JIS B5 edition for export."*

### 2. Creative Huddle Mode (Manual Writers' Room — `/huddle`)

When you want to brainstorm, test twists, debate competing story directions, or workshop character dilemmas **before** committing to production, explicitly activate **Creative Huddle Mode**:

- `/huddle` (or *"Start a creative huddle"*) — Opens a single-facilitator writers' room led by **Creative Lead**, consulting **Plot Architect**, **Character Psychologist**, **Story Critic**, and **Lore Researcher** *(acting as Mythology / Lore Advisor)*.
- Supports **`roundtable`** (default opening), **`debate`** (competing trade-offs without forced consensus), and **`workshop`** (tight interactive follow-ups).
- Persists concise session summaries in `manga/creative/huddle-session.yaml` and records explicitly approved choices in `manga/creative/decisions.yaml`—never auto-approving ideas or triggering production until you end the huddle (`/huddle end`) and separately authorize production.

See [`docs/CREATIVE-HUDDLE.md`](docs/CREATIVE-HUDDLE.md) for the complete writers' room guide.

---

## How Cursor Discovers Studio Components

| Layer | Location | How Cursor Uses It |
|---|---|---|
| **Root Orchestration** | `AGENTS.md` | Always loaded at the workspace root; defines Director routing, Huddle turn-start check, approval gates, and quality standards. |
| **Executive Team Subagents (4)** | `.cursor/agents/executive-team/*.md` | Studio leadership, quality gates & release governance (`manga-director`, `manga-editor`, `continuity-editor`, `publishing-director`). |
| **Production Team Subagents (8)** | `.cursor/agents/production-team/*.md` | Narrative, lore, character, script, storyboard, art direction, native illustration & lettering (`story-architect`, `lore-researcher`, `character-architect`, `manga-scriptwriter`, `storyboard-director`, `art-director`, `illustration-artist`, `lettering-artist`). |
| **Creative Team Subagents (4)** | `.cursor/agents/creative-team/*.md` | Writers'-room roles (`creative-lead`, `plot-architect`, `character-psychologist`, `story-critic`; reuses `lore-researcher` as Mythology/Lore Advisor). |
| **Studio Rules (7)** | `.cursor/rules/*.mdc` | `director-routing.mdc` applies globally (`alwaysApply: true`); `project-boundaries.mdc` scopes to `manga/**/*`; `creative-huddle.mdc` and 4 domain rules apply contextually. |
| **Studio Skills (21)** | `.cursor/skills/<name>/SKILL.md` | 15 production skills + 6 Creative Huddle skills loaded on demand with progressive-disclosure `references/`. |
| **Slash Commands (7)** | `.cursor/commands/*.md` | Optional shortcuts: `/director`, `/new-manga`, `/plan-arc`, `/create-chapter`, `/produce-pages`, `/review-project`, and `/huddle`. |

---

## Initialized Manga Repository Layout (Created Only in Clones via `/new-manga`)

The master template ships with **zero** `manga/` directory or active huddle sessions. When you run `/new-manga` inside a cloned manga repository, Manga Studio scaffolds:

```text
manga/
├── manga-manifest.yaml            # Reading direction (rtl/ltr), edition mode, JIS-B5 preset, canon policy
├── series-bible.md                # Premise, world rules, themes, story boundaries
├── creative/
│   ├── huddle-session.yaml        # Active/paused/closed Creative Huddle summary (created on /huddle)
│   ├── decisions.yaml             # Binding user-approved creative decisions (Creative Decision Log)
│   └── ideas/                     # Candidate, exploring, rejected, and deferred brainstorm notes
├── lore/                          # Provenance-tagged canon & historical dossiers
├── arcs/                          # Multi-chapter story arc blueprints (arc-XX-<arc-slug>.md)
├── characters/                    # Character bibles & continuity constraints (char-<slug>.md)
├── chapters/
│   └── ch-01/
│       ├── script.md              # Page-by-page & panel-by-panel script
│       ├── storyboard.md          # Panel grids, camera angles, RTL/LTR flow, balloon zones
│       └── lettering.md           # 100% editable dialogue, captions, SFX & reading order
├── art/
│   ├── art-direction.md           # Color palette + native monochrome ink/screentone standards
│   ├── concepts/                  # Exploratory unapproved drafts
│   ├── references/                # User-approved character & environment sheets (color/ & monochrome/)
│   ├── panels/                    # Generated panel/page illustrations (color/ & monochrome/)
│   ├── covers/                    # Chapter & volume covers
│   └── asset-log.yaml             # Verified file paths, prompts, reference inputs & revision history
├── production/
│   ├── production-tracker.yaml    # Artifact inventory, chapter status & quality gate records
│   ├── chronology.md              # In-universe timeline, knowledge, injury & prop ledger
│   ├── decisions.md               # Production & editorial arbitration log
│   └── reviews/                   # Continuity, canon, editorial & publication audit reports
└── exports/
    ├── color/                     # Full-color edition manifest & ordered pages
    └── monochrome/                # Monochrome edition manifest & ordered pages
```

---

## Creative Approvals & Artifact Lifecycle

- **Creative Huddle ideas**: `PROPOSED` -> `EXPLORING` -> `CANDIDATE` -> `APPROVED` (logged in `manga/creative/decisions.yaml`) | `REJECTED` | `DEFERRED`.
- **Production artifacts**: `draft` -> `ready-for-approval` -> `approved` -> `published`.
- **You hold final creative authority.** Nothing is locked, canon-modified, redesigned, or published without explicit user sign-off, and `approved` / `published` files are never silently overwritten.

---

## Documentation Index

- [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) — Template-repo model, native Cursor orchestration, memory layout, and dual-edition art architecture
- [`docs/CREATIVE-HUDDLE.md`](docs/CREATIVE-HUDDLE.md) — Complete Creative Huddle Mode (writers' room) guide, modes, lifecycle, and Cursor limitations
- [`docs/AGENT-ROUTING.md`](docs/AGENT-ROUTING.md) — Request-to-specialist routing matrix, parallel vs. sequential patterns, and role boundaries
- [`docs/WORKFLOWS.md`](docs/WORKFLOWS.md) — End-to-end production & ideation pipelines from clone initialization to CBZ/PDF/print readiness
- [`docs/BEGINNERS-GUIDE.md`](docs/BEGINNERS-GUIDE.md) — Plain-language guide to manga storytelling, layouts, ink/tones, and print terminology
