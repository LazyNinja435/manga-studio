---
name: idea-evaluation
description: Stress-test and score manga story ideas, plot twists, character turns, and arc concepts across narrative stakes, originality, emotional logic, thematic alignment, canon compatibility, and manga visual payoff—assigning clear lifecycle states without auto-approving. Use when critiquing or comparing candidate ideas in Creative Huddle Mode.
---

# Idea Evaluation

## Activation Guidance

Use inside **Creative Huddle Mode** whenever comparing competing `PROPOSED` / `EXPLORING` concepts, vetting a twist before promoting it to `CANDIDATE`, or answering *"Is this idea strong enough?"* / *"What's broken here?"*.

## Inputs

- One or more candidate ideas under review.
- Current `manga/creative/huddle-session.yaml`, locked `manga/creative/decisions.yaml`, and approved baselines (`manga/manga-manifest.yaml`, `manga/series-bible.md`, `manga/lore/*.md`, `manga/characters/*.md`).

## Procedure

1. **Evaluate Across Six Concrete Manga Craft Criteria**:
   - **Originality & Surprise**: Does it avoid telegraphing the twist too early or recycling stale tropes?
   - **Emotional Logic (Earned Payoff)**: Do character choices follow authentically from their desires, fears, flaws, and knowledge?
   - **Stakes & Irreversibility**: Does something meaningful and hard to undo change if this succeeds or fails?
   - **Structural & Pacing Fit**: Does it create strong manga serialization momentum (setups, midpoint shifts, page-turn hooks) without breaking world rules?
   - **Canon & Continuity Compatibility**: Does it honor `canon_policy` and `APPROVED` decisions—and if it departs from source tradition, is the departure clearly labeled?
   - **Visual Storytelling Potential**: Can key emotional/action beats be *shown* visually on manga pages rather than explained in exposition dumps?
2. **Invite Constructive Criticism (`story-critic` + Discipline Lens)**:
   - Require `story-critic` to surface at least one genuine weak spot or hidden consequence on leading ideas, paired with an actionable repair.
3. **Assign an Explicit Non-Final Lifecycle Recommendation**:
   - Recommend keeping an idea in `EXPLORING`, advancing it to `CANDIDATE`, parking it as `DEFERRED`, or discarding it as `REJECTED`.
   - Never unilaterally mark an idea `APPROVED`.

## Expected Outputs

- Crisp diagnostic scorecard or comparative summary identifying strongest hooks, specific flaws, concrete upgrades, and suggested lifecycle state (`EXPLORING` | `CANDIDATE` | `DEFERRED` | `REJECTED`).

## Collaboration Guidelines

- Distinguish **fatal structural flaws** (logic holes, broken character logic, unintended canon contradictions) from **subjective taste calls** (darker vs. lighter tone).
- Protect the creator's exciting kernel while surgically replacing weak execution mechanics.

## Validation

- [ ] Every evaluated idea receives specific craft feedback grounded in concrete story/character mechanics (no vague praise).
- [ ] At least one concrete improvement accompanies every critical flaw identified.
- [ ] Lifecycle states remain pre-approval until the creator explicitly approves.

## Failure Handling

- **Idea depends on unverified historical/mythological canon**: Pause definitive canon judgment, tag canon compatibility as `needs-lore-check`, and route a targeted question to `lore-researcher` without inventing facts.
- **Two ideas score equally high on different axes**: Suggest switching to **`debate`** mode (`creative-debate`) so the creator can pick which manga identity they prefer.
