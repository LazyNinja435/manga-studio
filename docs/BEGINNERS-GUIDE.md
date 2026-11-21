# Beginner's Guide to Manga Production

New to making manga? You do not need any prior manga industry knowledge to use **Manga Studio**—the Director and specialist agents handle technical layout, ink/color specs, and print geometry automatically. This guide explains the core terms you will see in scripts, storyboards, and reviews.

---

## 1. Reading Direction: Right-to-Left (`RTL`) vs. Left-to-Right (`LTR`)

- **Traditional Japanese Manga (`rtl`)**: Books open from the opposite side of Western novels (the spine is on the **right** when closed). On every page, your eye starts at the **top-right panel**, reads right-to-left across each row (tier), and moves top-to-bottom down the page. Inside a single panel, speech balloons are also read **top-right to bottom-left**.
- **Left-to-Right (`ltr`)**: Matches Western comics—top-left to bottom-right across panels and speech balloons.
- Manga Studio defaults to traditional **`rtl`** and also supports **`ltr`** in each manga clone's `manga/manga-manifest.yaml`.

---

## 2. Storyboarding & Page Pacing Terms

- ***Name* (ネーム / Pronounced "Neh-mu")**: The Japanese industry term for a manga **storyboard**—a rough page-by-page layout blueprint showing panel boxes, camera angles, character staging, and where speech bubbles go before final drawing starts.
- **Panel & Tier**: A **panel** (*koma*) is a single framed moment of time (always one clear action per panel). Horizontal rows of panels are called **tiers**.
- **Gutter**: The blank channel between panels. Clean rectangular gutters feel steady; slanted or broken gutters create speed, tension, or shock.
- ***Ma* (間)**: Intentional "breathing room"—using quiet, wordless panels of a character's expression, wind in trees, or an empty hallway so emotional moments sink in instead of rushing past.
- **Page-Turn Hook (*Hiki*)**: Placing a surprise, threat, or emotional punch on the page immediately **after** the reader turns a leaf, creating natural momentum.
- **Splash Page**: A dramatic single panel covering an entire page for major reveals, arrivals, or impacts.
- **Double-Page Spread (*Mihiraki*)**: One panoramic scene spanning two facing pages side-by-side for maximum spectacle. Important faces and speech balloons are kept clear of the center fold (**spine gutter**) so nothing gets lost in the book binding.

---

## 3. Full-Color vs. Traditional Monochrome Manga

Manga Studio treats **Full-Color** and **Monochrome** as two distinct artistic crafts—**never** converting a color image to grayscale!

- **Why Grayscale Conversion Fails**: Simply removing color saturation turns bright red, medium blue, and grass green into nearly the same muddy mid-gray, flattening depth and making action hard to read.
- **How Real Monochrome Manga Works**:
  - **Line Weight**: Thick, dynamic ink contours (*G-pen* style) pull foreground characters forward; fine lines (*Maru-pen* style) push background architecture and delicate facial details back.
  - ***Beta* (ベタ — Solid Black Spotting)**: Bold areas of pure black ink (dark hair, deep shadows, cloaks, night skies) give the page instant visual punch, accented by crisp white hair sheen (*tsuya beta*).
  - **Screentones**: Patterned dot/gradient shading sheets measured by density (e.g., `10%` light fabric tone, `30%` twilight tone, `60%` heavy shadow) used sparingly so pages stay crisp.
  - **Crosshatching & Speedlines**: Hand-drawn ink lines showing texture, grim atmosphere, motion blur, or radial focus (*shūchūsen*).
  - **Negative Space & *Nuki* (White Halo)**: Leaving pure white paper around focal silhouettes so characters pop cleanly off detailed backgrounds.

---

## 4. Character Sheets & Visual Continuity

- **Character Reference Sheet (Model Sheet)**: A clean, evenly lit visual chart showing a character from front, 3/4, side, and back views alongside key facial expressions and props. Once you approve a character's reference sheet, `illustration-artist` uses it to keep their face, hair, scars, and outfit consistent across every chapter.
- **180-Degree Rule (Axis of Action)**: Keeping two conversing or dueling characters on consistent left/right sides of the virtual camera so readers never get confused about who is facing whom.

---

## 5. Lettering & Sound Effects

- **Editable Lettering**: Keeping all dialogue, narration, and sound-effect text in structured files (`lettering.md`) separate from raw panel illustrations so wording can be edited, polished, or translated anytime without redrawing art.
- **Balloon Shapes**: Smooth ovals carry normal speech; spiky bursts carry shouts; scalloped/borderless text carries internal thoughts; rectangular boxes carry narrator captions.
- **Diamond Shaping**: Breaking dialogue lines so the middle lines are slightly wider than the top and bottom lines, allowing text to nestle naturally inside oval balloons.
- **SFX (*Giongo* & *Gitaigo*)**: Manga uses drawn sound effects both for audible sounds (*giongo*, like **CLANG** or **ZAAA** for rain) and silent emotional/atmospheric states (*gitaigo*, like **DOOOOOOM** for heavy tension or **SHIIIN** for dead silence).

---

## 6. Print Sizes & Digital Formats

- **`JIS-B5` (`182 × 257 mm`)**: Traditional Japanese manga magazine/deluxe page proportion (and Manga Studio's default). It scales down proportionally with zero cropping to **`JIS-B6` (`128 × 182 mm`)**, a classic collected book (*tankōbon*) size.
- **Bleed (`3 mm`)**: Extra artwork extending slightly past the final cut line (**trim**) so full-page splashes have no accidental white slivers after printing and cutting.
- **Safe Area (*Uchi-waku*)**: The inner rectangle (`150 × 220 mm` on B5) where all normal panel borders, speech balloons, and faces stay safe from trimming and book-spine curve.
- **CBZ & PDF**: `CBZ` (Comic Book ZIP) is a standard archive of numbered page images (`001.png`, `002.png`, ...) plus optional `ComicInfo.xml` metadata supported by virtually every manga reader app; `PDF` packages pages for universal viewing and print proofing.
