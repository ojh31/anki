# Anki Decks

This repo holds plain-text Anki import files, one file per course/topic at the repo root.

## Layout

Flat: `<course-slug>.txt` at the root. All flashcards for a given course go in one file.

Current files:
- `wfr.txt` — Wilderness First Responder

When adding a new course, create a new top-level `.txt` (short lowercase slug). Don't introduce subfolders.

## File format

Plain UTF-8 `.txt`, tab-separated, with `#key:value` header lines at the top. Reference: https://docs.ankiweb.net/importing/text-files.html

Template:

```
#separator:tab
#html:true
#notetype:Basic
#deck:<Deck Name>
#tags:<space-separated tags>
<front>\t<back>
<front>\t<back>
```

Notes on the format:
- `#separator:tab` — tabs are safer than commas because card content often contains commas. Fields in the body are separated by a literal tab character.
- `#html:true` — lets you use `<b>`, `<br>`, `<i>`, `<ul>`, etc. Without it, tags render as literal text.
- Newlines inside a field: use `<br>` (with `html:true`). Don't use real newlines — Anki treats them as row breaks.
- `#deck:<Name>` — Anki creates the deck if it doesn't exist. Use nested decks with `::`, e.g. `Wilderness First Responder::Assessment`.
- `#notetype:Basic` — standard front/back. Use `Basic (and reversed card)` if you want both directions.
- `#tags:` — space-separated, applied to every note in the file.

## Importing

Anki desktop → File → Import → pick the `.txt`. Anki reads the headers, shows a preview, and creates the deck if needed. Re-importing the same file updates existing notes when the front field matches (duplicate handling is configurable in the import dialog).

## Gotchas

- Don't wrap the whole line in quotes — tab-separated fields don't need quoting. Quoting is only for CSV-style delimiters.
- If a field genuinely needs a tab character, switch `#separator` to `Pipe` or `Semicolon` for that file.
- Em-dashes, accents, and other non-ASCII characters are fine — the file is UTF-8.
