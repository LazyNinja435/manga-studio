---
name: interactive-workshop
description: Run fast, focused, conversational back-and-forth Workshop turns in Creative Huddle Mode—refining one narrative, character, or twist problem incrementally with selective specialist input and concise creator-first responses. Use for follow-up Huddle turns or when /huddle workshop is active.
---

# Interactive Workshop

## Activation Guidance

Use inside **Creative Huddle Mode** when the user explicitly activates **`workshop`** mode (`/huddle workshop`) OR automatically as the default cadence for short interactive follow-up turns after an initial Roundtable or Debate.

## Inputs

- Creator's focused follow-up reaction, critique, or tweak (e.g., *"That twist feels too predictable"*, *"What if she only suspects him?"*).
- Current `manga/creative/huddle-session.yaml` (preserving active thread, `candidate_ideas`, and `rejected_ideas`).
- Locked `manga/creative/decisions.yaml`.

## Procedure

1. **Isolate One Problem at a Time**:
   - Zero in on the exact beat, motivation, clue, or line of tension the creator just reacted to—do not re-litigate the entire series bible.
2. **Use Adaptive Delegation (1–2 Specialists Max)**:
   - Summon **only** the specialist(s) that directly unlock this specific snag (e.g., *"Too predictable"* -> `story-critic` + `plot-architect`; *"Doesn't feel in-character"* -> `character-psychologist`; *"Would this break the myth?"* -> `lore-researcher`).
   - Do **not** run a full four-agent committee for a small iterative nudge.
3. **Iterate Without Defensiveness**:
   - Accept creator pushback immediately—never defend an earlier AI suggestion the creator disliked.
   - Build directly on the creator's instinct, offering 1–2 tightened refinements or a pointed "what if...?" pivot.
4. **Keep Momentum Conversational**:
   - Aim for concise, natural writers'-room dialogue (typically a short synthesis + 1–2 refined options + 1 crisp follow-up question), avoiding multi-page memos.
5. **Update Session State Lightly**:
   - Refresh `working_hypotheses`, `candidate_ideas` / `rejected_ideas`, and `next_discussion_point` in `manga/creative/huddle-session.yaml`.

## Expected Outputs

- Short, high-momentum conversational response advancing the single active creative problem.
- Incremental state update in `manga/creative/huddle-session.yaml`.

## Collaboration Guidelines

- Match the creator's pace: short prompt -> focused response; deep reaction -> targeted deeper dive.
- Carry prior rejections forward so the room never re-proposes an angle the creator already killed.
- Prompt for explicit promotion (`CANDIDATE` -> `APPROVED`) only when an idea feels genuinely ready, never pushily.

## Validation

- [ ] Focused strictly on the single narrative snag at hand without sprawling essays.
- [ ] Specialist calls were selective and proportionate (not all agents summoned reflexively).
- [ ] Prior Huddle context and rejections were respected.

## Failure Handling

- **Workshop uncovers a much bigger structural fork**: Ask the creator if they want to switch briefly to **`debate`** or **`roundtable`** mode to weigh the bigger fork before zooming back in.
- **Refinement starts drifting into full chapter dialogue scripting**: Pause and remind the creator that Huddle stays at concept/beat level—offer to lock the concept as an approved decision and switch to `/create-chapter` after exiting the Huddle.
