# Provenance Taxonomy & Source Hierarchy Reference

## Four-Tier Provenance Tags

Use these exact tags in `lore/*.md` dossiers, character bibles, and canon audit reports:

| Tag | Meaning | Citation Requirement |
|---|---|---|
| `confirmed-primary` | Explicitly present in the project's locked primary baseline source/edition. | Cite verified work/section; if exact verse/line is not checked verbatim, note `(episode verified; exact verse unverified)`. |
| `attested-variant` | Attested in a named secondary recension, regional epic, later commentary, or folk tradition rather than the primary baseline. | Name the specific variant tradition and describe how it diverges from `confirmed-primary`. |
| `uncertain-disputed` | Ambiguous in primary sources, debated among historians/scholars, or not verifiable with confidence in the current environment. | Explain the ambiguity and list plausible interpretations without declaring certainty. |
| `creative-adaptation` | Original manga invention—composite scenes, inferred private conversations, visual motifs, or approved departures from canon. | Document dramatic rationale and confirm alignment with `manga/manga-manifest.yaml` `canon_policy`. |

## Project `canon_policy` Modes

- **`strict-canon`**: Follow `confirmed-primary` closely; allow `creative-adaptation` only in silent interstitial beats that never contradict primary events, vows, chronology, or characterizations.
- **`faithful-adaptation`**: Preserve core plot milestones, themes, and characterizations of `confirmed-primary`; may weave in selected `attested-variant` details or dramatic compression with Director/user approval.
- **`inspired-reimagining`**: Uses canonical figures/myths as a springboard for bold structural or thematic reinvention; still tracks departures honestly in `lore/` so internal project canon stays consistent.
- **`original-fiction`**: World and cast are studio-original; `lore/` tracks internal world history, factions, and magic/tech rules with the same internal consistency rigor.
