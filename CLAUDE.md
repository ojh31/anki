# Anki Decks

This repo holds plain-text Anki import files, one file per course/topic at the repo root.

## Layout

Flat: `<course-slug>.txt` at the root. All flashcards for a given course go in one file.

Current files:
- `wfr.txt` — Wilderness First Responder (NOLS curriculum — use NOLS terminology and frameworks, e.g. the three-phase Patient Assessment System)

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

## Atomicity

Cards should be strictly atomic: **one concept, acronym, or fact per card**. When in doubt, split.

- **Split** distinct items that just happen to be taught together. PPE and BSI are two acronyms — two cards. MOI and NOI — two cards.
- **Keep as one** a mnemonic or short checklist that's learned and used as a single unit. SAMPLE, AVPU, the 4 P's of Safety, and the four "assess the numbers" questions each stay as one card — splitting them destroys the mnemonic/checklist structure.

Test: if someone knowing half the card would still have a useful mental unit, split it. If they'd just have a fragment, keep it together.

## Editing vs. adding

Before adding cards, scan the target `.txt` for overlap. If a concept is already covered, **edit the existing card** rather than creating a near-duplicate. Duplicates fragment the user's review history and confuse spaced-repetition scheduling.

- Same question, better wording → edit the existing card.
- Same topic, new facet the old card doesn't cover → add a new atomic card for the new facet, leave the old one alone.
- Old card was wrong → edit it.

## Importing

Anki desktop → File → Import → pick the `.txt`. Anki reads the headers, shows a preview, and creates the deck if needed. Re-importing the same file updates existing notes when the front field matches (duplicate handling is configurable in the import dialog).

## Gotchas

- Don't wrap the whole line in quotes — tab-separated fields don't need quoting. Quoting is only for CSV-style delimiters.
- If a field genuinely needs a tab character, switch `#separator` to `Pipe` or `Semicolon` for that file.
- Em-dashes, accents, and other non-ASCII characters are fine — the file is UTF-8.
