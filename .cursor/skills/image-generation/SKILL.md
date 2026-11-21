---
name: image-generation
description: Generate manga character sheets, concept art, backgrounds, panels, splashes, and covers using Cursor's native built-in image generation tool with strict reference passing, balloon-safe framing, disk verification, and asset-log provenance. Use only when visual asset generation is explicitly requested.
---

# Native Image Generation

## Purpose

Execute reliable, reference-consistent visual asset generation inside Cursor using **only** Cursor's built-in image generation capability—maintaining full provenance, versioned revisions, and verified disk outputs without external APIs or servers.

## Inputs

- Explicit request for visual asset creation (reference sheet, concept, panel, splash, or cover).
- `manga/art/art-direction.md` and relevant `manga/characters/*.md` / `manga/chapters/ch-XX/storyboard.md`.
- Approved reference image paths from `manga/art/references/` and `manga/art/asset-log.yaml`.

## Procedure

1. **Check Native Tool Availability**:
   - Inspect Cursor's built-in `cursor` dynamic tool namespace via `GetDynamicTools` (specifically `GenerateImage`) to verify availability and exact supported parameters (`description`, `filename`, `reference_image_paths`, `aspect_ratio`).
   - Do **not** invoke image generation during workspace setup, text-only planning, or script reviews.
2. **Gather Visual References**:
   - Collect verified file paths from `manga/art/references/` for every recurring character, outfit, weapon, or environment in the frame to pass in `reference_image_paths`.
3. **Select Aspect Ratio & Framing**:
   - Choose the supported `aspect_ratio` matching the asset (`3:4` for vertical B5-proportioned pages, splashes, covers, and standing sheets; `4:3` or `16:9` for wide horizontal panels or double-page spread concepts; `1:1` for close-up expression/prop callouts).
   - Reserve clean negative space in the zones specified by `storyboard.md` and instruct **no speech bubbles, captions, or embedded dialogue text** unless cover/logo lettering is explicitly requested.
4. **Construct Edition-Specific Description**:
   - Combine: `[Edition medium & style rules from art-direction.md]` + `[Shot scale, camera angle, composition & reserved dead-space]` + `[Subject visual anchors matching reference_image_paths]` + `[Single frozen action & expression]` + `[Lighting/ink-tone treatment]`.
   - Generate **color** and **monochrome** editions via separate calls with medium-specific descriptions.
5. **Invoke, Verify on Disk & Organize**:
   - Invoke `GenerateImage`, then immediately verify the output file exists on disk (e.g., via `Glob` / `Read`).
   - Organize or copy verified assets into `manga/art/{concepts,references,panels,covers}/{color,monochrome}/` using versioned naming (`ch01-p03-pan02-v1.png`)—never overwriting approved files.
6. **Record Provenance**:
   - Append an entry to `manga/art/asset-log.yaml` capturing asset ID, path, edition, tool used, prompt, `reference_image_paths`, aspect ratio, revision number, and `approval_status`.

## Output

- Verified image file(s) under `manga/art/`
- Updated `manga/art/asset-log.yaml`

## Validation

- [ ] Every reported image path has been verified to exist on disk.
- [ ] `reference_image_paths` included approved character/environment sheets wherever applicable.
- [ ] Panel art contains no unwanted baked dialogue bubbles and preserves storyboard balloon zones.
- [ ] Prior versions and `approved` assets remain untouched on disk.

## Failure Handling

- **`GenerateImage` unavailable or blocked in active session**: Stop immediately—do not install external packages, call third-party APIs, or claim images were created. Record prepared prompts in `art/asset-log.yaml` with `status: prompt-prepared` and report tool unavailability clearly.
- **Visual drift or anatomy/prop defect**: Retain `-v1` in `concepts/` or revision history, refine the description + reference emphasis, generate `-v2`, and document what was corrected.
