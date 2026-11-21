---
name: huddle
description: Manually activate, switch modes in, inspect, pause, resume, or end Creative Huddle Mode (conversational writers' room facilitated by Creative Lead)
---

> Convenience shortcut: Explicit natural-language triggers invoke this same protocol—e.g. *"Start a creative huddle"* / *"Enter huddle mode"* / *"Let's have a writers' room discussion"* (activate), *"Switch to roundtable"* (roundtable), *"Debate these options"* (debate), *"Let's workshop this beat"* (workshop), *"Show huddle status"* (status), *"Pause the huddle"* (pause), *"Resume the huddle"* (resume), and *"End the huddle"* / *"Exit creative mode"* (end). Casual questions or quick brainstorming must **never** silently activate persistent Huddle Mode.

Interpret `$ARGUMENTS` conversationally as the **Manga Director** (`AGENTS.md`) routing into or managing **Creative Huddle Mode** (`.cursor/rules/creative-huddle.mdc` + `.cursor/skills/creative-huddle/SKILL.md`):

## Supported Conversational Subcommands

Cursor slash commands pass trailing text as `$ARGUMENTS` rather than native CLI subcommand flags. Interpret the leading keyword in `$ARGUMENTS` cleanly:

- **`/huddle`** (no argument or opening topic) -> Activate Creative Huddle Mode in default **`roundtable`** mode (or resume if paused), greet conversationally as **Creative Lead** (*"Creative Huddle is active. What would you like to explore?"*), and consult creative specialists if a topic was already supplied.
- **`/huddle roundtable [topic]`** -> Activate or switch to **Roundtable** mode (parallel independent specialist perspectives synthesized by Creative Lead).
- **`/huddle debate [topic]`** -> Activate or switch to **Debate** mode (assigned competing positions with honest trade-offs and no forced consensus).
- **`/huddle workshop [topic]`** -> Activate or switch to **Workshop** mode (short, focused, interactive back-and-forth on one narrative challenge at a time).
- **`/huddle status`** -> Report current session state (`active` / `paused` / `closed`), mode, topic, active candidates, approved decisions, and open questions from `manga/creative/huddle-session.yaml`.
- **`/huddle pause`** -> Set `status: paused` in `manga/creative/huddle-session.yaml` so ordinary Director production routing can run temporarily without losing Huddle context.
- **`/huddle resume`** -> Restore a `paused` session to `status: active` and pick up from `next_discussion_point`.
- **`/huddle end`** -> Summarize the session, confirm approved decisions are logged in `manga/creative/decisions.yaml`, preserve candidate/deferred ideas and open questions, set `status: closed` in `manga/creative/huddle-session.yaml`, and return future turns to ordinary **Manga Director** mode **without** starting production automatically.

## Core Execution & Safety Rules

1. **Master Template Guard**: Confirm this repository is an initialized manga clone (or that the user explicitly intends to brainstorm inside a cloned manga repo). **Never** write `manga/creative/huddle-session.yaml` inside the master `manga-studio` template repository.
2. **Single-Facilitator Voice**: Operate through **Creative Lead** (`.cursor/agents/creative-team/creative-lead.md`, or parent Agent following the Creative Lead protocol with native specialist delegation across turns). Consult `plot-architect`, `character-psychologist`, `story-critic`, and `lore-researcher` (as Mythology / Lore Advisor) selectively as needed.
3. **Creator Authority & Separation from Production**: Keep ideas in explicit lifecycle states (`PROPOSED` -> `EXPLORING` -> `CANDIDATE` -> `APPROVED` | `REJECTED` | `DEFERRED`). Never auto-approve ideas, never trigger chapter writing, artwork generation, or publishing during or upon exiting Huddle Mode.
