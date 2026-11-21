---
name: creative-debate
description: Facilitate structured Creative Debate in Huddle Mode—assigning genuinely competing creative positions across specialists, surfacing trade-offs, consequences, canon tensions, and risks without forcing artificial consensus. Use when the creator runs /huddle debate or needs to weigh tough narrative forks.
---

# Creative Debate

## Activation Guidance

Use inside **Creative Huddle Mode** when the user activates **`debate`** mode (`/huddle debate`), faces a high-stakes narrative fork (e.g., *"Should Character X betray the protagonist now or in Arc 3?"*, *"Stay strictly canonical or invent a secret faction?"*), or asks specialists to argue competing options.

## Inputs

- The contested creative question or 2–3 competing `EXPLORING` / `CANDIDATE` options.
- Active `manga/creative/huddle-session.yaml` and `manga/creative/decisions.yaml`.
- Relevant approved story/canon constraints (`manga/manga-manifest.yaml`, `manga/lore/*.md`, `manga/series-bible.md`).

## Procedure

1. **Sharpen the Debate Axis**:
   - State the exact decision fork in one sentence so specialists argue the real trade-off rather than talking past each other.
2. **Assign Competing Positions Explicitly**:
   - Assign distinct specialists (or lenses) to champion opposing or contrasting sides—for example:
     - `plot-architect` argues high-momentum structural payoff (Option A).
     - `character-psychologist` argues slower, emotionally earned burn (Option B).
     - `story-critic` attacks hidden blind spots in **both** options and tests whether a sharper Option C exists.
     - `lore-researcher` *(Mythology / Lore Advisor)* evaluates canonical authenticity vs. adaptation liberty when source material applies.
3. **Run Independent Arguments (Parallel)**:
   - Require every position to name: (a) strongest narrative payoff, (b) immediate consequence for upcoming chapters, (c) biggest structural/emotional/canon risk.
4. **Synthesize Trade-Offs Without Fake Consensus**:
   - Present the clash transparently as Creative Lead: where the room agrees, where specialists genuinely disagree, and what kind of manga each choice creates.
   - Do **not** paper over conflict with a watered-down compromise unless a genuine synthesis clearly beats both options.
5. **Invite the Creator's Verdict**:
   - Ask the creator whether to lock one side (`APPROVED`), promote one to `CANDIDATE` for further testing, hybridize, or reject both.

## Expected Outputs

- Crisp, balanced Creative Debate summary highlighting competing positions, consequences, and unresolved trade-offs.
- Updated `working_hypotheses`, `candidate_ideas`, or `open_questions` in `manga/creative/huddle-session.yaml`.

## Collaboration Guidelines

- Disagreement is a feature—protect sharp, honest tension between Plot, Character Psychology, Canon, and Story Critic.
- Never let a specialist strawman the competing option; steelman every side before critiquing it.
- Keep the final debate synthesis scannable so the creator can compare options in seconds.

## Validation

- [ ] Every debated option shows concrete strengths, downstream consequences, and honest risks.
- [ ] Disagreements are preserved transparently—zero forced artificial consensus.
- [ ] No option is marked `APPROVED` until the creator explicitly decides.

## Failure Handling

- **Specialists accidentally converge on the same answer**: Task `story-critic` explicitly with arguing the strongest counter-case against the consensus before reporting to the creator.
- **Canon constraint makes one side violate `strict-canon`**: Flag the canon conflict explicitly as a boundary warning rather than hiding the creative option; let the creator choose whether to honor canon or revisit `canon_policy`.
