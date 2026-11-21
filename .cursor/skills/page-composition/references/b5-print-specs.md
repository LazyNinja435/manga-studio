# Manga Page Presets & JIS B5 Print Specifications

## Primary Studio Presets

| Preset ID | Trim Size (W × H) | Full Canvas w/ 3 mm Bleed | Inner Safe / Live Frame | Typical Use |
|---|---|---|---|---|
| `JIS-B5` *(Default)* | `182 × 257 mm` | `188 × 263 mm` | `150 × 220 mm` | Japanese manga manuscript / anthology / deluxe edition |
| `JIS-B6` | `128 × 182 mm` | `134 × 188 mm` | `104 × 154 mm` | Seinen / standard collected tankōbon trim (scales cleanly from B5!) |
| `ISO-A5` | `148 × 210 mm` | `154 × 216 mm` | `120 × 180 mm` | Kanzenban / international digital-print editions |
| `US-Manga-Trim` | `127 × 191 mm` (5 × 7.5 in) | `133 × 197 mm` | `102 × 165 mm` | English trade paperback manga |

*Why `JIS-B5` is the studio default*: B5 (`182 × 257 mm`, aspect ratio `1 : 1.412`) shares the exact \(\sqrt{2}\) proportional ratio of `JIS-B6` (`128 × 182 mm`), allowing lossless proportional scaling between magazine/deluxe B5 and pocket tankōbon B6.

## Pixel Resolution Reference (`JIS-B5` w/ 3 mm Bleed = `188 × 263 mm`)

- **Monochrome Print Target (600 DPI)**: `4441 × 6213 px` (minimum `350 DPI`: `2591 × 3624 px`)
- **Full-Color Print Target (350 DPI)**: `2591 × 3624 px`
- **Digital Reading Export (150–200 DPI equiv.)**: `1400 × 1980 px`

## Binding Direction & Recto/Verso Parity

- **Traditional Japanese (`rtl`)**:
  - Book spine is on the **right** when closed; pages turn from left to right.
  - Inside spread pairs place the **earlier** page on the **right** and the **later** page on the **left**.
  - Big page-turn reveals belong on the **right-hand opening** after turning a left-hand page (verify whether Chapter Page 1 opens on a single left-side page after an inside title/ad, which is standard in Japanese serialization so Page 2–3 can form the first spread).
- **Left-to-Right (`ltr`)**:
  - Book spine is on the **left** when closed; pages turn from right to left.
  - Inside spread pairs place the **earlier (even)** page on the **left** and the **later (odd)** page on the **right**.
