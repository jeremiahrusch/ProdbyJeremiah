# ProdbyJeremiah — Agent Instructions

## Project overview
Static GitHub Pages site that displays free beat packs. Pack data lives entirely in `packs.json`. There is no backend — editing `packs.json` and pushing to `main` is how the site is updated.

## Adding a new pack

When the user says "add a pack" or gives pack details, edit `packs.json` by appending a new entry to the JSON array. Use this shape:

```json
{
  "id": "kebab-case-name",
  "name": "Pack Display Name",
  "artist": "ProdbyJeremiah",
  "genre": "Trap",
  "bpm": "140",
  "desc": "Short description of what's inside.",
  "cover": "<thumbnail URL or null>",
  "file": "<Google Drive / Dropbox link or null>"
}
```

### Field rules
- `id` — auto-generate from `name`: lowercase, spaces and special chars replaced with `-`, strip leading/trailing `-`. Must be unique across all entries.
- `artist` — default to `"ProdbyJeremiah"` unless told otherwise.
- `genre` — must be one of: `"Trap"`, `"R&B"`, `"Underground"`, `"One Shots"`. Ask if unclear.
- `bpm` — string, e.g. `"140"` or `"80–95"`. Leave `""` if not provided.
- `desc` — keep it concise (1–2 sentences). Leave `""` if not provided.
- `cover` — paste the URL exactly as given. If it's a Google Drive share link, leave it as-is (the site doesn't transform cover URLs). Use `null` if none.
- `file` — paste the URL exactly as given. Google Drive folder/file share links work as-is. Use `null` if none.

### What to ask the user for
If any required field is missing, ask before editing:
1. Pack name (required)
2. Genre (required)
3. Google Drive download link (can be null, but ask)
4. Thumbnail/cover image link (can be null)
5. BPM range (optional)
6. Description (optional)

### After editing packs.json
Remind the user to commit and push to GitHub so the live site updates:
```
git add packs.json
git commit -m "Add <pack name> pack"
git push
```

## Removing a pack
Delete the matching object from the array in `packs.json`. Confirm the pack name before deleting.

## Editing a pack
Update only the specified fields. Do not change the `id` unless the user explicitly asks, as it may affect download count tracking stored in localStorage by that id.

## Genre filter pills
The site has hardcoded filter pills for `Trap`, `R&B`, and `Underground`. If a new genre is needed, it must also be added to the `filter-pills` section in `index.html`.

## File structure
- `index.html` — entire frontend (HTML + CSS + JS, single file)
- `packs.json` — array of pack objects, the only data file
- `packs/` — empty folder, not used by the site
