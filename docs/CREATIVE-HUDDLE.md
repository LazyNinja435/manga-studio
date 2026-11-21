# Creative Huddle Mode (AI Writers' Room)

**Creative Huddle Mode** is an AstrAI-inspired collaborative writers' room built directly on Manga Studio's native Cursor architecture. While the **Production Studio** focuses on drafting scripts, storyboards, artwork, lettering, and print packages, **Creative Huddle Mode** gives the human creator a dedicated, conversational space to brainstorm, stress-test twists, debate competing story directions, and sharpen character psychology **without** prematurely locking decisions or triggering production.

---

## 1. Purpose & Creative Firewall

Use Creative Huddle Mode for:
- Brainstorming series hooks, arc concepts, mysteries, and chapter ideas
- Exploring character dilemmas, flaws, betrayals, and emotional payoffs
- Debating competing narrative forks and testing plot twists against reader expectations
- Identifying plot holes, weak stakes, predictability, and canon tensions early

**Strict Production Firewall:**
- The human creator remains the final creative authority.
- Discussing, refining, or even approving an idea inside a Huddle **never** auto-initiates chapter scripting, storyboarding, image generation, or publishing.
- Exiting a Huddle returns control to ordinary **Manga Director** routing without launching production automatically.

---

## 2. Single-Facilitator Orchestration Model

```text
HUMAN CREATOR
      │
      ▼
MANGA DIRECTOR (Default entry point: AGENTS.md + director-routing.mdc)
      │
      │ Manual Huddle activation (/huddle or explicit trigger)
      ▼
CREATIVE LEAD (.cursor/agents/creative-team/creative-lead.md)
      │
      ├── Plot Architect           (.cursor/agents/creative-team/plot-architect.md) [read-only]
      ├── Character Psychologist   (.cursor/agents/creative-team/character-psychologist.md) [read-only]
      ├── Story Critic             (.cursor/agents/creative-team/story-critic.md) [read-only]
      ├── Mythology / Lore Advisor (Reuses .cursor/agents/production-team/lore-researcher.md)
      └── Selective production advisors (art-director, storyboard-director, continuity-editor) only when needed
```

- **One conversational voice**: Specialists return their discipline-specific insights to **Creative Lead**, who synthesizes them cleanly for the creator—never flooding the chat with independent walls of text from every agent.
- **No unnecessary agent duplication**: The **Mythology / Lore Advisor** role routes directly to the existing `lore-researcher` agent rather than creating a redundant lore agent.
- **No recursive delegation**: `manga-director -> creative-lead -> manga-director` loops are explicitly prohibited.

### Creative Lead Responsibilities

**Creative Lead** acts as an experienced manga writers'-room facilitator (not an automated script generator):

- **Listen & steer**: Understand the creator's creative instinct, ask sharp clarifying questions, and preserve discussion momentum.
- **Coordinate specialists adaptively**: Select only the specialists needed for the current turn (`plot-architect`, `character-psychologist`, `story-critic`, `lore-researcher`), running independent analyses in parallel when useful and synthesizing them into one cohesive voice.
- **Encourage originality & honest critique**: Surface genuinely distinct directions and protect constructive disagreement rather than rubber-stamping predictable ideas.
- **Manage idea lifecycle & memory**: Track `PROPOSED`, `EXPLORING`, `CANDIDATE`, `REJECTED`, and `DEFERRED` states in `manga/creative/huddle-session.yaml` (concise summaries only), and record `APPROVED` commitments in `manga/creative/decisions.yaml` **only** after explicit creator sign-off.
- **Protect the production firewall**: Never prematurely finalize choices, never overwrite approved production files mid-huddle (flag downstream impacts instead), and never launch scripting, artwork, or publishing automatically.

---

## 3. Manual Activation & Subcommands

Huddle Mode **never** activates silently during ordinary questions or casual remarks. Activation requires an explicit user trigger:

### Slash Command (`.cursor/commands/huddle.md`)

Cursor slash commands accept trailing text via `$ARGUMENTS`, which the Director/Creative Lead interprets conversationally:

| Command | Behavior |
|---|---|
| `/huddle` | Activate Creative Huddle Mode in default **`roundtable`** mode (or resume if paused) and greet as Creative Lead. |
| `/huddle roundtable [topic]` | Switch to or start **Roundtable** mode for multi-perspective exploration. |
| `/huddle debate [topic]` | Switch to or start **Debate** mode with competing specialist positions and explicit trade-offs. |
| `/huddle workshop [topic]` | Switch to or start **Workshop** mode for concise, rapid iterative back-and-forth on one problem. |
| `/huddle status` | Show current session status, mode, active candidates, approved decisions, and open questions. |
| `/huddle pause` | Pause the Huddle (`status: paused`) so normal production commands can run without losing brainstorming context. |
| `/huddle resume` | Resume a paused Huddle (`status: active`) from `next_discussion_point`. |
| `/huddle end` | Summarize, preserve candidate/deferred ideas, close session (`status: closed`), and return to Manga Director mode. |

### Natural-Language Equivalents

- **Activate**: *"Start a creative huddle."*, *"Let's have a writers' room discussion."*, *"Enter huddle mode."*
- **Exit**: *"End the huddle."*, *"Exit creative mode."*, *"Let's stop brainstorming."*

---

## 4. Three Huddle Discussion Modes

You can switch modes at any time while a Huddle is active:

1. **`roundtable` (Default Opening Mode)**
   - Creative Lead selects relevant specialists (`plot-architect`, `character-psychologist`, `story-critic`, and `lore-researcher` when canon matters).
   - Independent perspectives can run in parallel; Creative Lead synthesizes 2–4 distinct directions and asks which thread the creator wants to pull.
2. **`debate`**
   - Creative Lead assigns genuinely competing positions across specialists (e.g., high-momentum structural payoff vs. slow-burn emotional earn, with `story-critic` exposing blind spots in both).
   - Disagreement is preserved transparently—zero forced artificial consensus—leaving the trade-off verdict to the creator.
3. **`workshop` (Default for Short Interactive Follow-Ups)**
   - After an initial Roundtable, short follow-up turns naturally settle into **Workshop** cadence: tight, conversational back-and-forth focused on one narrative snag at a time, summoning only 1–2 targeted specialists rather than writing long reports on every turn.

---

## 5. Persistent Session State (Cloned Manga Repos Only)

Active Huddle state lives inside each cloned manga repository at:

- **`manga/creative/huddle-session.yaml`** *(scaffolded from `templates/huddle-session.yaml`)*
- **`manga/creative/decisions.yaml`** *(scaffolded from `templates/creative-decision-log.yaml`)*
- **`manga/creative/ideas/`** *(optional notes for larger candidate or deferred concepts)*

The master `manga-studio` template repository **never** stores active huddle sessions or manga-specific decisions.

**What `huddle-session.yaml` stores:** `session_id`, `status` (`active` | `paused` | `closed`), `manga_slug`, `mode`, `topic`, `started_at`, `last_updated`, `participants`, `working_hypotheses`, `candidate_ideas`, `approved_decisions`, `rejected_ideas`, `deferred_ideas`, `open_questions`, and `next_discussion_point`. It stores concise structured summaries only—never raw chat transcripts.

On every turn, `AGENTS.md` and `.cursor/rules/director-routing.mdc` instruct the parent Agent to check `manga/creative/huddle-session.yaml`:
- If `status: active` -> continue Creative Lead facilitation and keep the session file updated.
- If absent, `paused`, or `closed` -> follow normal Manga Director routing.

---

## 6. Idea Lifecycle & Creator Approval Rules

Every concept in a Huddle carries an explicit state:

| State | Meaning | Binding Canon? |
|---|---|---|
| `PROPOSED` | Fresh brainstorming spark introduced by creator or specialist. | No |
| `EXPLORING` | Actively being fleshed out, questioned, or iterated. | No |
| `CANDIDATE` | Strong contender ready for creator judgment. | No |
| `APPROVED` | Explicitly accepted by the creator and logged in `manga/creative/decisions.yaml`. | **Yes** *(Story Canon)* |
| `REJECTED` | Explicitly discarded by the creator (recorded to prevent recycling). | No |
| `DEFERRED` | Interesting idea parked for a later arc or future huddle. | No |

- **Explicit approval required**: Only clear creator authorization (*"I approve option 2"*, *"Lock this idea"*, *"Make this official"*) moves an idea into `manga/creative/decisions.yaml`. Ambiguous remarks trigger a 1-line confirmation check.
- **Story canon vs. source canon**: Each approved decision records `canon_type` (`story-canon`, `source-canon-alignment`, or `approved-canon-departure`) so invented fiction is never confused with verified mythological/historical source canon (`manga/lore/`).
- **Non-destructive impact flagging**: If a newly approved decision affects existing approved production files (`series-bible.md`, `arcs/`, `characters/`), Creative Lead records `revision_flags` rather than silently overwriting production artifacts mid-huddle.

---

## 7. Exiting Huddle Mode & Relationship to Production Studio

Running `/huddle end` (or saying *"End the huddle"*):
1. Summarizes the session's breakthroughs and decisions.
2. Confirms all creator-approved commitments are stored in `manga/creative/decisions.yaml`.
3. Preserves `CANDIDATE`, `DEFERRED`, and `REJECTED` ideas plus `open_questions` in `manga/creative/huddle-session.yaml`.
4. Marks `status: closed`.
5. Returns future turns to normal **Manga Director** routing and may suggest—**never automatically invoke**—a next production step (e.g., `/plan-arc`, character bibles, or `/create-chapter`).

When you later run production workflows, `story-architect`, `character-architect`, `manga-scriptwriter`, and `continuity-editor` read `manga/creative/decisions.yaml` as binding creative constraints.

---

## 8. Honest Limitations of Native Cursor Orchestration

Manga Studio uses zero custom orchestration daemons, MCP servers, or runtime wrappers. Keep three native Cursor realities in mind:

1. **File-backed persistence, not an IDE-enforced mode lock**: Huddle session persistence works because `AGENTS.md` and `director-routing.mdc` instruct the Agent to check `manga/creative/huddle-session.yaml` on every turn. Cursor itself does not guarantee an independent native mode switch outside the agent reading that file.
2. **Parent Agent emulates multi-turn Creative Lead continuity**: Cursor subagents run per `Task` invocation rather than persistently owning the top-level chat loop across turns. Therefore, the parent Cursor Agent executes the Creative Lead conversational loop across turns while delegating specialized analytical passes (`plot-architect`, `character-psychologist`, `story-critic`, `lore-researcher`) natively.
3. **Team-grouped `.cursor/agents/<team>/*.md` discovery**: All 16 studio agents are organized into `.cursor/agents/{executive-team,creative-team,production-team}/*.md` and discovered by their `name` frontmatter slug. If an un-reloaded session or older Cursor version does not expose a nested slug in the `Task` tool, the parent Agent transparently runs the Creative Team protocols via available native subagents without fabricating calls.
