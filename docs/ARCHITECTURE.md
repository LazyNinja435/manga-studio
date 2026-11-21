# Manga Studio Architecture

## 1. Design Philosophy: Template Repository + Native Cursor Runtime

Manga Studio is a **reusable Cursor-native template repository**—not an application server and not a multi-project monorepo. Each manga is created by cloning this repository into its own independent Git repository. There are zero custom orchestration daemons, Node/Python runtimes, MCP servers, React dashboards, databases, or external image APIs.

```text
User Prompt (Natural Language or optional /command)
        │
        ▼
┌────────────────────────────────────────────────────────────────────┐
│ Parent Cursor Agent                                                │
│ Governed by: AGENTS.md + .cursor/rules/director-routing.mdc        │
│ Checks manga/creative/huddle-session.yaml at turn start            │
└───────────┬────────────────────────────────────┬───────────────────┘
            │ Active Huddle (/huddle)            │ Default Production Mode
            ▼                                    ▼
┌───────────────────────────────┐    ┌───────────────────────────────┐
│ Creative Huddle Mode          │    │ Production Studio             │
│ Creative Lead (Single Voice)  │    │ Manga Director                │
│  ├─ plot-architect [ro]       │    │  ├─ story-architect           │
│  ├─ character-psychologist[ro]│    │  ├─ lore-researcher           │
│  ├─ story-critic [ro]         │    │  ├─ character-architect       │
│  └─ lore-researcher (reused)  │    │  ├─ manga-scriptwriter        │
│                               │    │  ├─ storyboard-director       │
│ Writes ONLY: manga/creative/  │    │  ├─ art-director              │
│ Never auto-starts production  │    │  ├─ illustration-artist       │
└───────────────────────────────┘    │  ├─ lettering-artist          │
                                     │  ├─ continuity-editor [ro]    │
                                     │  ├─ manga-editor [ro]         │
                                     │  └─ publishing-director       │
                                     └──────────────┬────────────────┘
                                                    │ Reads / Writes isolated
                                                    ▼
                                     ┌───────────────────────────────┐
                                     │ manga/ (Clone-Only Memory)    │
                                     │ Manifest, Bibles, Creative,   │
                                     │ Chapters, Art, Production     │
                                     └───────────────────────────────┘
```

---

## 2. Template Sync Boundary (Master Repo vs. Manga Clones)

To keep future studio improvements easy to merge into active manga repositories without overwriting manga-specific content:

| Ownership Tier | Paths | Present in Master Template? | Sync Strategy |
|---|---|---|---|
| **Template-Owned Studio Core** | `AGENTS.md`, `.cursor/agents/`, `.cursor/rules/` (studio rules), `.cursor/skills/`, `.cursor/commands/`, `templates/`, `docs/`, `README.md` | Yes | Never store manga-specific plot, cast, or huddle data here; pull cleanly via `git merge template/main`. |
| **Manga-Owned Repository Data** | `manga/**` (`manga-manifest.yaml`, `series-bible.md`, `creative/`, `lore/`, `arcs/`, `characters/`, `chapters/`, `art/`, `production/`, `exports/`) | **No** (created only via `/new-manga` in a clone) | Lives exclusively inside each cloned manga repository; zero upstream merge conflict. |
| **Clone-Local Rule Overrides** *(optional)* | `.cursor/rules/local-*.mdc` | **No** | Safe namespace for series-specific Cursor rules inside a clone without touching template rules. |

---

## 3. Two-Layer Orchestration & Honest Platform Boundaries

Cursor's root `AGENTS.md` governs the parent chat Agent, while `.cursor/agents/{executive-team,creative-team,production-team}/*.md` defines specialist subagents invoked via the `Task` tool. Because a custom subagent file cannot technically replace Cursor's parent conversation loop across turns:

1. **Parent Cursor Agent (`AGENTS.md` + `director-routing.mdc`)** acts as the live entry point on every turn—serving as the **Manga Director** by default, or emulating the **Creative Lead** conversational facilitator across turns whenever `manga/creative/huddle-session.yaml` has `status: active` (and delegating specialist tasks natively).
2. **Delegated Subagent Teams (`.cursor/agents/`)**:
   - **`.cursor/agents/executive-team/` (4)**: `manga-director.md` (multi-phase planning & arbitration; never recursively self-delegating), `manga-editor.md` (`readonly`), `continuity-editor.md` (`readonly`), and `publishing-director.md`.
   - **`.cursor/agents/production-team/` (8)**: `story-architect.md`, `lore-researcher.md`, `character-architect.md`, `manga-scriptwriter.md`, `storyboard-director.md`, `art-director.md`, `illustration-artist.md`, and `lettering-artist.md`.
   - **`.cursor/agents/creative-team/` (4)**: `creative-lead.md`, `plot-architect.md` (`readonly`), `character-psychologist.md` (`readonly`), and `story-critic.md` (`readonly`)—with `lore-researcher.md` reused cleanly as the **Mythology / Lore Advisor**.
   - **Discovery note**: Cursor recursively discovers team-grouped `.cursor/agents/<team>/*.md` files and indexes each specialist by its `name` frontmatter slug. If an older Cursor build or un-reloaded session has not yet indexed a nested slug, the parent Agent transparently follows that specialist's protocol via available tools without fabricating subagent calls.
3. **File-backed Huddle persistence**: Persistence across turns is an agent instruction-following convention backed by `manga/creative/huddle-session.yaml`, not an IDE-enforced modal switch.

---

## 4. Specialist Roster & Platform-Enforced Read-Only Guardrails

All 16 subagents use only officially documented Cursor YAML frontmatter (`name`, `description`, and `readonly: true` where appropriate):

- **Authoring & Production Specialists (10)**: `manga-director`, `story-architect`, `lore-researcher`, `character-architect`, `manga-scriptwriter`, `storyboard-director`, `art-director`, `illustration-artist`, `lettering-artist`, `publishing-director`.
- **Creative Huddle Facilitator (1)**: `creative-lead` (writes only under `manga/creative/`).
- **Platform-Enforced Read-Only Advisors & Auditors (5)**: `continuity-editor`, `manga-editor`, `plot-architect`, `character-psychologist`, and `story-critic` all declare `readonly: true`. This prevents unapproved file edits and enables safe parallel audits and parallel writers'-room perspectives with zero write contention.

---

## 5. Contextual Rules & Progressive-Disclosure Skills

- **Always-On Rule (1)**: Only `.cursor/rules/director-routing.mdc` sets `alwaysApply: true` to keep baseline context lean.
- **File-Scoped Rule (1)**: `.cursor/rules/project-boundaries.mdc` scopes via `globs: manga/**/*` so single-manga boundaries, template-sync hygiene, and artifact lifecycle rules engage automatically on manga files.
- **Contextual Rules (5)**: `agent-orchestration.mdc`, `creative-huddle.mdc`, `canon-integrity.mdc`, `visual-consistency.mdc`, and `quality-gates.mdc` set `alwaysApply: false` with targeted descriptions.
- **Skills (21)**: 15 production skills + 6 Creative Huddle skills (`creative-huddle`, `creative-brainstorming`, `creative-debate`, `interactive-workshop`, `idea-evaluation`, `creative-decision-log`), with 4 progressive-disclosure reference guides under `references/`.

---

## 6. File-Based Manga Memory & Write Isolation (Inside Clones)

| Memory Domain | Canonical File Location | Primary Writer |
|---|---|---|
| Manga config & format | `manga/manga-manifest.yaml` | `story-architect` / Director |
| Series memory & world rules | `manga/series-bible.md` | `story-architect` |
| Huddle session & approved creative decisions | `manga/creative/{huddle-session.yaml,decisions.yaml,ideas/}` | `creative-lead` (approved decisions only on explicit user sign-off) |
| Canon & provenance | `manga/lore/*.md` | `lore-researcher` |
| Long-range narrative arcs | `manga/arcs/arc-XX-<arc-slug>.md` | `story-architect` |
| Character memory & invariants | `manga/characters/char-<slug>.md` | `character-architect` |
| Chapter script, layout & text | `manga/chapters/ch-XX/{script,storyboard,lettering}.md` | `manga-scriptwriter`, `storyboard-director`, `lettering-artist` |
| Visual style & asset provenance | `manga/art/art-direction.md`, `manga/art/asset-log.yaml`, `manga/art/{concepts,references,panels,covers}/` | `art-director`, `illustration-artist` |
| Chronology, gates & production decisions | `manga/production/{production-tracker.yaml,chronology.md,decisions.md,reviews/}` | Director (synthesizing specialist handoffs) |
| Edition packages | `manga/exports/{color,monochrome}/` | `publishing-director` |

**Concurrency rule:** Parallel subagents may read shared baselines simultaneously, but two concurrent subagents never write to the same target file path.

---

## 7. Dual-Edition & Native Image Architecture

- **True Dual-Edition Craft**: Full-Color and Monochrome editions share `script.md`, `storyboard.md`, `lettering.md`, and character identities while applying medium-native artistic execution (`art/.../color/` vs. `art/.../monochrome/`). Monochrome artwork uses black ink line weights, solid black (*beta*) spotting, crosshatching, screentones, and white negative space—never grayscale conversion.
- **Native Cursor Image Generation**: `illustration-artist` verifies Cursor's built-in `GenerateImage` tool (`cursor` dynamic namespace), passes approved `reference_image_paths`, keeps dialogue text out of raw panel images so `lettering.md` remains editable, verifies generated files on disk, and logs provenance in `manga/art/asset-log.yaml`.
