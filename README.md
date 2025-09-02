# Norway National Parks — Two SVGs (basemap + parks+labels)

This site uses **basemap.svg** (static background) and **national_parks_lable.svg** (parks + labels in one file).
Click a park to toggle green + bold label. Light zoom (1×–4×).

## Run locally
```
python -m http.server 8080
# open http://localhost:8080/
```

## Deploy (GitHub Pages)
- Push the files in this folder to your repo root.
- Settings → Pages → Deploy from branch → (default branch) → root → Save.

## Pairing logic
For each park polygon we try, in order:
1) **Name match:** compare the polygon's title/id/data-name to label text (case/diacritics-insensitive).
2) **Contains test:** if a label sits *inside* the polygon (uses `SVGGeometryElement.isPointInFill`), pair it.
3) **Nearest label:** fallback to the closest label in screen space.

If some labels still mismatch, ensure each polygon has a `<title>` with the correct park name and that label text matches.
