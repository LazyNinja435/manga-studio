---
name: lettering
description: Create editable manga lettering blueprints specifying RTL or LTR balloon sequence, oval/diamond line shaping, balloon styles, captions, SFX typography, and safe-margin placement without baking dialogue destructively into panel artwork. Use when lettering chapters or auditing dialogue readability.
---

# Manga Lettering

## Purpose

Produce structured, 100% editable chapter lettering specifications (`manga/chapters/ch-XX/lettering.md`) that guide reader eye movement cleanly across balloons, captions, and sound effects while protecting underlying artwork and supporting effortless revisions or localization.

## Inputs

- `manga/manga-manifest.yaml` (`reading_direction`, `page_preset`, `language`).
- `manga/chapters/ch-XX/script.md` and `storyboard.md`.
- Optional: Panel illustrations in `manga/art/panels/` to verify exact negative-space placement.
- Workspace-root template: `templates/lettering-script.md`.

## Procedure

1. **Index Strict Reading Sequence**:
   - Assign sequential `order` numbers (`1, 2, 3...`) per page and per panel matching `reading_direction`:
     - **`rtl`**: Top-right -> bottom-left within each panel; tail points cleanly toward speaking character's mouth/chest (or inward tick for off-panel speakers).
     - **`ltr`**: Top-left -> bottom-right within each panel.
   - Never cross balloon tails or place a second speaker's balloon higher/earlier on the reading axis than the first speaker's line.
2. **Enforce Word Budgets & Diamond Line Shaping**:
   - Keep individual balloons concise (<= 20–25 words ideal). Break longer speeches into two linked sequential balloons (`1a -> 1b`) at a natural breath pause.
   - Format line breaks in a balanced oval/diamond profile (shorter top/bottom lines, wider middle lines) so text sits centered inside oval/vertical-oval manga balloons without ragged single-word orphans.
3. **Assign Balloon & Typography Roles**:
   - `speech-normal`: Clean smooth oval (vertical oval preferred for traditional manga pacing; horizontal rounded oval for wide horizontal space).
   - `speech-shout`: Spiky burst (`uni-flash` / jagged border), bold display emphasis.
   - `speech-whisper`: Dashed or thin hairline contour with generous inner whitespace.
   - `thought-internal`: Soft scalloped/feather border, borderless floating text over tone, or clean caption box per `art-direction.md`.
   - `caption-narration`: Crisp rectangular box (single or double border) anchored near panel edge.
   - `sfx`: Hand-drawn/expressive vector-style sound cue specifying phonetic text, visual weight, curve/angle following action motion, and optional micro-gloss note.
4. **Verify Visual & Margin Clearance**:
   - Confirm placement coordinates match `storyboard.md` reserved balloon zones, clear all faces/eyes/hands/focal weapons, and stay inside the inner safe margin (`uchi-waku`).

## Output

- `manga/chapters/ch-XX/lettering.md`

## Validation

- [ ] Every line of dialogue, thought, caption, and SFX in `script.md` is accounted for verbatim and remains plain editable text.
- [ ] Balloon sequence strictly follows `reading_direction` with zero crossed tails or inverted speaker order.
- [ ] No single balloon exceeds comfortable manga readability limits (~25 words) without a linked split or trim flag.
- [ ] All live text clears trim edges and spine gutters.

## Failure Handling

- **Dialogue exceeds panel's reserved dead space**: Propose a 2-balloon split first; if still cramped, flag exact panel/line to `manga-scriptwriter` (for line tightening) or `storyboard-director` (for panel expansion) rather than shrinking font below readable print size.
- **Panel artwork accidentally occupied reserved balloon zone**: Adjust balloon anchor to secondary negative space if clean; otherwise flag a targeted panel revision to `illustration-artist`.
