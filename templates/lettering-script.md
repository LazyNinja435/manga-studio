---
artifact_type: lettering-script
manga_slug: "<manga-slug>"
chapter_id: "ch-01"
reading_direction: "rtl" # rtl | ltr
page_preset: "JIS-B5"
editable_text_master: true
version: "0.1"
status: "draft" # draft | ready-for-approval | approved
---

# Editable Lettering Blueprint — Chapter `<XX>`

> Keep all dialogue, captions, thoughts, and SFX editable in this master file. Do not bake body dialogue destructively into raw panel artwork.

## Typography & Balloon Role Key

- `speech-normal`: Smooth vertical/oval balloon, standard dialogue font
- `speech-shout`: Jagged burst border, bold display emphasis
- `speech-whisper`: Thin/dashed contour, smaller point size with wide inner margin
- `thought-internal`: Scalloped/borderless floating monologue over tone
- `caption-narration`: Rectangular box anchored inside safe frame (`uchi-waku`)
- `sfx`: Expressive sound effect following motion curve (include phonetic + gloss note)

---

## Page 01 Lettering Map (`Reading Order: 1 -> N` in `rtl` / `ltr`)

| Order | Panel | Element Type | Speaker / Source | Placement Zone & Tail Direction | Diamond-Shaped Editable Text | Notes |
|---|---|---|---|---|---|---|
| `1` | `1.1` | `caption-narration` | Narrator | Upper-right safe corner (`no tail`) | `<Line 1>`<br>`<Wider Line 2>`<br>`<Line 3>` | Inside `150x220mm` safe frame |
| `2` | `1.1` | `sfx` | Wind / Environment | Sweeping `R -> L` across upper sky, behind foreground | `<ZAAA...>` | Gloss: *(rushing wind)* |
| `3` | `1.2` | `speech-normal` | `<Character A>` | Top-right reserved zone; tail -> `<Character A>` mouth | `<Short line 1>`<br>`<Middle line 2>`<br>`<Short line 3>` | `<= 25 words` verified |
| `4` | `1.3` | `speech-shout` | `<Character B>` | Top-left reserved zone; tail -> `<Character B>` | `<Impact line!>` | Clears blade & eyes |
