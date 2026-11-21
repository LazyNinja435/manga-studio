---
name: creative-huddle
description: Orchestrate and sustain Creative Huddle Mode—managing manual activation, file-backed session state in manga/creative/huddle-session.yaml, Roundtable/Debate/Workshop mode transitions, single-facilitator specialist synthesis, and clean session closure. Use when activating, continuing, pausing, resuming, or ending Creative Huddle Mode.
---

# Creative Huddle Orchestration

## Activation Guidance

Use **only** when the user explicitly activates or manages Creative Huddle Mode (`/huddle`, *"Start a creative huddle"*, *"Enter huddle mode"*, *"End the huddle"*) or when `manga/creative/huddle-session.yaml` already exists with `status: active`. Never load this skill to hijack ordinary production prompts or casual one-off questions.

## Inputs

- User prompt, topic, or subcommand (`roundtable`, `debate`, `workshop`, `status`, `pause`, `resume`, `end`).
- `manga/creative/huddle-session.yaml` (if an active or paused session exists) and `manga/creative/decisions.yaml`.
- Optional story context (read selectively only when relevant): `manga/manga-manifest.yaml`, `manga/series-bible.md`, `manga/lore/*.md`, `manga/characters/*.md`, `manga/arcs/*.md`.
- Workspace-root templates: `templates/huddle-session.yaml` and `templates/creative-decision-log.yaml`.

## Procedure

1. **Check Repository Guard & Current Session State**:
   - Confirm this workspace is a manga repository (not the uninitialized master template repo). If `manga/manga-manifest.yaml` does not exist and this appears to be the master template repo, ask before creating `manga/creative/`.
   - Read `manga/creative/huddle-session.yaml` if present.
2. **Handle Session Lifecycle Actions**:
   - **Activate (`new`)**: Create `manga/creative/huddle-session.yaml` from workspace-root `templates/huddle-session.yaml` with `status: active` and default `mode: roundtable` (unless user specified `debate` or `workshop`). If no topic was provided, respond warmly and concisely as Creative Lead: *"Creative Huddle is active. What would you like to explore?"*
   - **Continue (`active`)**: Preserve prior `working_hypotheses`, `candidate_ideas`, `approved_decisions`, `rejected_ideas`, `deferred_ideas`, and `open_questions`. After an initial `roundtable`, naturally default short iterative follow-ups to **`workshop`** mode unless the user requests another `roundtable` or `debate`.
   - **Switch Mode**: Update `mode` in `huddle-session.yaml` (`roundtable` | `debate` | `workshop`) and apply the matching mode skill (`creative-brainstorming`, `creative-debate`, or `interactive-workshop`).
   - **Pause / Resume**: Toggle `status: paused` <-> `status: active` without losing session context.
   - **End (`/huddle end`)**: Summarize the session, confirm all user-approved choices are recorded in `manga/creative/decisions.yaml`, retain candidate/deferred ideas and open questions, set `status: closed`, return future turns to normal **Manga Director** routing, and optionally suggest (never auto-launch) a next workflow.
3. **Coordinate Specialists via Single Facilitator**:
   - Select only the specialists needed for the current turn (`plot-architect`, `character-psychologist`, `story-critic`, `lore-researcher` as Mythology / Lore Advisor, or an existing production specialist for narrow feasibility questions).
   - Run independent specialist perspectives in parallel when helpful, then synthesize them in **Creative Lead's** single conversational voice.
4. **Update Structured Session Summary**:
   - Update `manga/creative/huddle-session.yaml` with concise bullets (`last_updated`, `participants`, idea states, `open_questions`, `next_discussion_point`). Never store verbatim chat transcripts.

## Expected Outputs

- Conversational Creative Lead facilitation response (clear options, sharp questions, brief state note).
- Updated `manga/creative/huddle-session.yaml` (in cloned manga repos).
- Updated `manga/creative/decisions.yaml` **only** when the user explicitly approves a decision.

## Collaboration Guidelines

- Never let multiple agents reply separately to the user; **Creative Lead** synthesizes every turn.
- Keep responses punchy and dialogue-driven so the creator stays in creative flow.
- Keep `story-critic` honest—never sand off real disagreements before presenting options.
- Respect the firewall: discussing or approving an idea never starts scripting, artwork, or publishing.

## Validation

- [ ] Activation was explicitly triggered by the user (or resumed from an already `active` session file).
- [ ] `manga/creative/huddle-session.yaml` contains concise structured state (zero raw transcripts).
- [ ] Approved decisions are stored separately from `PROPOSED`/`EXPLORING`/`CANDIDATE`/`REJECTED`/`DEFERRED` ideas.
- [ ] Exiting Huddle sets `status: closed` and launches zero production tasks.

## Failure Handling

- **Nested Creative Team subagents not indexed in active Cursor session**: Execute the Creative Lead facilitation protocol directly in the parent Agent and delegate independent specialist lenses via available native subagents (`lore-researcher`, `generalPurpose` loaded with the `.cursor/agents/creative-team/*.md` persona) without fabricating missing subagent calls.
- **User tries to run a production task mid-huddle (e.g., *"Write chapter 1 now"*)**: Offer to `/huddle pause` or `/huddle end` first so creative exploration and formal production stay cleanly separated.
