---
name: canon-research
description: Research mythological, historical, literary, or franchise source material; classify claim provenance; compare primary and regional variants; validate timelines; and document uncertainties without fabricating citations. Use when working on source-based, historical, or canon-governed manga.
---

# Canon Research

## Purpose

Build verifiable, citation-honest lore dossiers (`manga/lore/*.md`) and canon validation reports that separate primary source facts, attested variants, scholarly ambiguity, and studio creative adaptations.

## Inputs

- Research prompt and `canon_policy` from `manga/manga-manifest.yaml`.
- User-provided texts, notes, or existing `manga/lore/*.md` files.
- Workspace-root template: `templates/canon-dossier.md`.
- Reference guide: [references/provenance-taxonomy.md](references/provenance-taxonomy.md).

## Procedure

1. **Identify Source Hierarchy**:
   - Check `manga/manga-manifest.yaml` or `manga/series-bible.md` for the designated primary baseline tradition/text and permitted secondary traditions.
2. **Gather & Cross-Check Claims**:
   - Inspect workspace source documents first; use available read-only search/reference tools only if needed and available.
   - Extract plot events, chronology, genealogies, vows/laws, geography, attire, architecture, and weaponry relevant to visual and script accuracy.
3. **Classify Every Entry by Provenance** (see [references/provenance-taxonomy.md](references/provenance-taxonomy.md)):
   - `confirmed-primary`
   - `attested-variant`
   - `uncertain-disputed`
   - `creative-adaptation`
4. **Verify Citations Strictly**:
   - Record exact book/section/verse numbers **only** when directly verified. Whenever exact locus cannot be confirmed verbatim, record the broader known episode/tradition and tag exact locus as `[exact citation unverified]`.
5. **Surface Contradictions & Visual Hooks**:
   - Document conflicts across variants and highlight concrete material-culture details useful for `character-architect` and `art-director`.

## Output

- `manga/lore/<topic-slug>.md` (dossier) or structured canon audit / Huddle advisory notes.

## Validation

- [ ] Every factual/canonical assertion has one of the four provenance tags.
- [ ] Zero fabricated citations, invented quotes, or guessed verse numbers appear anywhere.
- [ ] Timeline order and variant divergences are explicitly separated.
- [ ] Practical implications for story, character, and art teams are summarized concisely.

## Failure Handling

- **Primary text unavailable locally or online**: State clearly which claims come from general literary/historical knowledge vs. verified primary text, mark exact citations `[unverified — primary text check recommended]`, and never guess locus numbers.
- **Irreconcilable source variants**: Present the competing traditions neutrally with dramatic trade-offs so the Director and user can select the project's canonical baseline.
