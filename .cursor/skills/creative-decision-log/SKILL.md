---
name: creative-decision-log
description: Record explicitly user-approved creative decisions in manga/creative/decisions.yaml—maintaining strict separation between binding approved story decisions, unapproved ideas, and source canon while flagging downstream impacts on existing approved production files. Use when the creator explicitly approves, locks, rejects, or defers an idea in Creative Huddle Mode.
---

# Creative Decision Log

## Activation Guidance

Use inside **Creative Huddle Mode** whenever the creator explicitly authorizes a creative choice (e.g., *"I approve this"*, *"Let's go with option 2"*, *"Make this official"*, *"Lock this idea"*) or explicitly discards/defers a candidate so session memory stays crisp and accurate.

## Inputs

- Explicit user approval, rejection, or deferral statement and the exact referenced idea.
- `manga/creative/huddle-session.yaml` and `manga/creative/decisions.yaml` (scaffolded from workspace-root `templates/creative-decision-log.yaml`).
- Existing approved production files (`manga/series-bible.md`, `manga/arcs/*.md`, `manga/characters/*.md`, `manga/lore/*.md`) to check for downstream impact.

## Procedure

1. **Verify Unambiguous Approval**:
   - Confirm *exactly* which option or statement the user approved. If the referent is ambiguous (e.g., *"Sure, sounds good"* after three competing options), ask a 1-line confirmation before logging an `APPROVED` decision.
2. **Separate Binding Decisions from Unapproved Ideas**:
   - **Approved (`APPROVED`)**: Append a structured entry to `manga/creative/decisions.yaml` with:
     - `decision_id` (e.g., `CDEC-001`)
     - `topic`
     - `decision`
     - `status: approved`
     - `canon_type`: `story-canon` (original fictional commitment) vs. `source-canon-alignment` / `approved-canon-departure` (for source-based manga)
     - `reasoning_summary`
     - `related_ideas`
     - `affected_characters`, `affected_arcs`, `affected_chapters`
     - `revision_flags` (list any existing `approved` production files that will later need updating)
     - `approved_by: user`
     - `approved_at: <YYYY-MM-DD>`
   - **Rejected (`REJECTED`) / Deferred (`DEFERRED`)**: Record in `manga/creative/huddle-session.yaml` (and optionally `manga/creative/ideas/`) so they remain searchable without becoming binding canon.
3. **Sync Session Summary**:
   - Mirror the new `decision_id` into `approved_decisions` inside `manga/creative/huddle-session.yaml` and clear it from `candidate_ideas`.
4. **Flag Downstream Impacts Without Silently Rewriting**:
   - If the newly approved decision contradicts or extends an already-approved `series-bible.md`, arc, or character bible, explicitly surface `revision_flags` so the creator can later authorize the owning production specialist (`story-architect`, `character-architect`, etc.) to update those files.
   - Keep the Huddle active and do **not** launch production automatically.

## Expected Outputs

- Updated `manga/creative/decisions.yaml` (binding approved decisions only).
- Updated `manga/creative/huddle-session.yaml` reflecting the new state transition.
- Brief confirmation to the creator stating the logged `decision_id`, any downstream revision flags, and inviting the next creative topic.

## Collaboration Guidelines

- Never promote `CANDIDATE` -> `APPROVED` based solely on specialist enthusiasm.
- Never conflate fictional story decisions (`story-canon`) with verified mythological or historical facts (`source-canon`).
- When superseding a previously approved creative decision, mark the earlier entry `superseded` (referencing the new `decision_id`) rather than erasing history.

## Validation

- [ ] Every `APPROVED` entry has an unambiguous user authorization, `decision_id`, `canon_type`, and affected-entity fields.
- [ ] Rejected and deferred ideas are kept completely out of binding `approved` decision entries.
- [ ] Existing approved production files were **not** silently rewritten during the Huddle.

## Failure Handling

- **Ambiguous approval phrasing**: Quote the specific option in one sentence and ask *"Want me to lock Option 2 into the decision log?"* before writing to `decisions.yaml`.
- **`manga/creative/decisions.yaml` does not exist yet (in a cloned manga repo)**: Initialize it cleanly from workspace-root `templates/creative-decision-log.yaml` first. (Never create it in the master template repository.)
