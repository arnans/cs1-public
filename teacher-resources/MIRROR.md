# Mirror: this folder is a published copy, not the source

Everything in this `teacher-resources/` folder is **copied in from the
book-cs1 repo** (`teacher-resources/`, plus each chapter's
`teacher-guide/renders/` and `slides/renders/`). Do not hand-edit files here
except for the one deliberate divergence noted below — changes will be
overwritten the next time this folder is re-synced from book-cs1, and won't
exist upstream.

```
book-cs1/teacher-resources/          (source of truth)
        │  manual copy
        ▼
cs1-public/teacher-resources/        (this folder — published copy)
        │  git push → GitHub Pages
        ▼
https://arnans.github.io/cs1-public/teacher-resources/
```

## The one deliberate divergence

`index.html` here is **not byte-identical** to the source. In book-cs1 the
download links use a `../` prefix (chapter folders sit beside
`teacher-resources/`, one level up). Here the chapter folders live *inside*
`teacher-resources/`, so the two link templates drop the `../`:

```js
const guideHref = `${ch.dir}/teacher-guide/renders/${ch.guideBase}${suffix}.docx`;
const href = `${ch.dir}/slides/renders/${s.base}${suffix}.pptx`;
```

Everything else (the `CHAPTERS` data — titles, session bases, file sizes)
must match the book-cs1 source exactly.

## videos/ — no divergence

`videos/` (the demo-video index, added 2026-07-09) is **byte-identical** to
the book-cs1 source: its thumbnails live in its own `videos/thumbs/`, fonts
resolve via `../fonts/` in both layouts, and there are no download links yet
(clips are still being filmed — every card shows a "coming soon" state).
Future video links will be external (YouTube / `d.gogoboard.org/v-*`), so
this subfolder never needs the link-prefix edit — sync it with a plain
`cp -r`.

## How to re-sync from book-cs1

When book-cs1 re-renders teacher guides or slides, or edits `index.html`:

```bash
SRC="path/to/book-cs1"
DST="path/to/cs1-public/teacher-resources"
cp "$SRC/teacher-resources/index.html" "$DST/index.html"
# re-apply the `../` -> `` link-prefix edit above in $DST/index.html
cp -r "$SRC/teacher-resources/fonts" "$SRC/teacher-resources/thumbs" "$SRC/teacher-resources/videos" "$DST/"
for ch in ch01-what-is-coding ch02-sensors-and-conditions ch03-interactive-games ch04-ai-control; do
  cp "$SRC/$ch/teacher-guide/renders/"*.docx "$DST/$ch/teacher-guide/renders/"
  cp "$SRC/$ch/slides/renders/"*.pptx "$DST/$ch/slides/renders/"
done
```

Then verify every link in the new `index.html` resolves to a file of the
expected size (parse `CHAPTERS` out of the HTML, `fs.statSync` each path)
before committing and pushing. GitHub Pages redeploys 1-2 minutes after
push.

This is a manual process — there's no automation tying the two repos
together. See `MIRROR.md` in book-cs1's `teacher-resources/` for the same
note from the source side.
