---
name: director
description: Route any creative, production, review, or status request through the Manga Director orchestration workflow
---

> Convenience shortcut: Ordinary natural-language prompts automatically follow this exact Manga Director workflow without needing `/director`.

Act as the **Manga Director** (`AGENTS.md`) and process the user's request (`$ARGUMENTS` or current prompt):

1. **Check Creative Huddle state first**: If `manga/creative/huddle-session.yaml` exists with `status: active`, stay in Creative Huddle Mode unless the user explicitly pauses or ends the huddle.
2. **Verify manga repository context**: Check `manga/manga-manifest.yaml`. If absent and the user wants to start a new manga inside a fresh clone of this template repository, guide or invoke `/new-manga` (never initialize `manga/` inside the master template repository itself).
3. **Inspect relevant artifacts**: Read `manga/manga-manifest.yaml`, `manga/creative/decisions.yaml` (if present), `manga/production/production-tracker.yaml`, and only the approved bibles/scripts/references needed for the request.
4. **Select specialists & skills**:
   - Route to matching `.cursor/agents/{executive-team,production-team}/*.md` specialists (`manga-director`, `story-architect`, `lore-researcher`, `character-architect`, `manga-scriptwriter`, `storyboard-director`, `art-director`, `illustration-artist`, `continuity-editor`, `lettering-artist`, `manga-editor`, `publishing-director`) or `.cursor/agents/creative-team/` when Huddle Mode is explicitly invoked.
   - Load matching `.cursor/skills/*/SKILL.md` procedures.
5. **Execute cleanly**: Run independent workstreams in parallel and dependent steps sequentially with single-writer isolation and `.cursor/rules/quality-gates.mdc` checks.
6. **Synthesize & report**: Update `manga/production/` records as appropriate, present results concisely, highlight user approval gates, and propose clear next actions.
