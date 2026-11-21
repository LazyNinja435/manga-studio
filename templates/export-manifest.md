---
artifact_type: export-manifest
manga_slug: "<manga-slug>"
package_scope: "ch-01" # ch-XX | vol-XX
edition: "monochrome" # color | monochrome
reading_direction: "rtl" # rtl | ltr
page_preset: "JIS-B5"
status: "ready-for-approval" # draft | blocked | ready-for-approval | published
---

# Edition Export Manifest — `<Package Scope>` (`<Edition>`)

## 1. Upstream Quality Gate Verification

- **Story / Arc Gate**: `<passed>`
- **Canon Gate**: `<passed | not-applicable>`
- **Continuity Gate**: `<passed>`
- **Visual Consistency Gate**: `<passed>`
- **Lettering Gate**: `<passed>`
- **Editorial Review Gate**: `<passed>`

## 2. Print & Digital Specifications

- **Page Preset**: `JIS-B5` (`182 × 257 mm` trim; `188 × 263 mm` w/ `3 mm` bleed; `150 × 220 mm` safe area)
- **Color / Ink Profile**: `<Full-Color (sRGB digital / CMYK print notes) | Native Monochrome Ink & Screentones (never desaturated color)>`
- **Editable Text Archive**: `chapters/<ch-XX>/lettering.md` + `chapters/<ch-XX>/script.md`
- **CBZ Metadata (`ComicInfo.xml`)**: `Manga="<YesAndRightToLeft | No>"`

## 3. Ordered Page & Spread Sequence

| Archive Filename | Story Page(s) | Side (`RTL` / `LTR`) | Type | Verified Source Asset Path |
|---|---|---|---|---|
| `000-cover.png` | Cover | Front | Cover | `art/covers/<edition>/ch-01-cover.png` |
| `001.png` | Page 01 | `<left | right>` | Single | `art/panels/<edition>/ch-01-p01.png` |
| `002-003-spread.png` | Pages 02–03 | Facing Pair | Spread | `art/panels/<edition>/ch-01-p02-03-spread.png` |
