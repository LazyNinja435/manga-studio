---
name: creative-brainstorming
description: Run divergent multi-perspective Roundtable brainstorming in Creative Huddle Mode—generating genuinely distinct story premises, arcs, twists, mysteries, and character concepts across Plot Architect, Character Psychologist, Story Critic, and Lore Advisor. Use during Roundtable Huddle turns or whenever generating fresh narrative alternatives.
---

# Creative Brainstorming (Roundtable Method)

## Activation Guidance

Use inside **Creative Huddle Mode** (primarily **`roundtable`** mode, or when a **`workshop`** needs fresh divergent options) when the creator introduces a seed idea, asks *"What could happen next?"*, or wants multiple creative directions before narrowing down.

## Inputs

- Creator's seed idea, theme, premise, or narrative problem.
- Current `manga/creative/huddle-session.yaml` and locked `manga/creative/decisions.yaml`.
- Relevant canon/world guardrails from `manga/manga-manifest.yaml`, `manga/series-bible.md`, and `manga/lore/*.md` (when present).

## Procedure

1. **Frame the Creative Prompt Without Pre-Solving It**:
   - Identify the single core dramatic spark the creator cares about plus any hard constraints (genre, tone, `canon_policy`, already `APPROVED` decisions).
2. **Gather Independent Specialist Lenses (Parallel Where Useful)**:
   - **`plot-architect`**: Generate 2–3 structurally distinct mechanisms (different root causes, reveal timings, or escalation engines—never three slight variations of the same trope).
   - **`character-psychologist`**: Explore what emotional flaw, hidden loyalty, or moral dilemma each direction unlocks for key characters.
   - **`lore-researcher`** *(Mythology / Lore Advisor)*: *If source-based/historical*, highlight mythic resonance, canonical anchors to preserve, and creative liberty boundaries.
   - **`story-critic`**: Flag the most obvious cliché trap up front and suggest one unexpected angle that subverts reader expectations.
3. **Synthesize into 2–4 Distinct Creative Directions**:
   - Present each direction with a memorable name, core hook, emotional/structural upside, and biggest trade-off/risk.
   - Tag new ideas as `PROPOSED` (or `EXPLORING` if building on an active thread).
4. **Hand the Wheel Back to the Creator**:
   - Ask 1–2 focused steering questions (*"Which direction has the emotional charge you want—or should we splice Option A's twist with Option C's motive?"*).

## Expected Outputs

- A tight, high-signal Roundtable synthesis presenting 2–4 genuinely differentiated creative directions.
- Concise `PROPOSED` / `EXPLORING` additions in `manga/creative/huddle-session.yaml`.

## Collaboration Guidelines

- Diverge before converging: resist jumping straight to a single "recommended answer."
- Ensure each specialist contributes a distinct discipline lens instead of echoing another specialist.
- Protect originality—if an option echoes a cliché the user wants to avoid, replace it rather than padding the list.

## Validation

- [ ] At least 2–3 options differ in core narrative or psychological mechanism (not surface window-dressing).
- [ ] Every option respects locked `APPROVED` decisions and flags any canon departure explicitly.
- [ ] All newly generated options remain `PROPOSED` / `EXPLORING`—never auto-promoted to `APPROVED`.

## Failure Handling

- **Creator's seed is very broad (e.g., *"I want a cool villain"*)**: Offer 3 sharply contrasted archetypes anchored in different thematic conflicts, then ask which vibe clicks before drilling deeper.
- **Creator rejects every proposed direction**: Log discarded ideas as `REJECTED` (so the room stops recycling them), ask what felt wrong about them, and pivot axes (e.g., shift from external conspiracy to intimate betrayal).
