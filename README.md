# Image Swapper

A batch image converter that resizes, crops, compresses, and re-encodes
images to JPG, PNG, or WEBP — entirely in the browser. Nothing is uploaded
anywhere; every conversion runs on-device via the Canvas API. Live at [promptcutter.com](https://www.imageswapper.com).

## What it does

- Drag-and-drop or file-picker intake of multiple images at once (accepts
  JPG, PNG, WEBP, GIF, and BMP as input)
- An interactive crop tool — draggable, resizable selection box — applied
  per image before export
- A quality slider for JPEG/WEBP (PNG always stays lossless)
- Configurable export "rows": define multiple output sizes per image by
  scale factor, fixed width, or fixed height — similar to Figma's
  @1x/@2x/@3x export presets — each with its own filename suffix and choice
  of output format(s)
- A live before/after preview (Original vs. Optimized), modeled on
  Photoshop's "Save for Web," showing the exact file-size delta as the
  quality/size settings change
- Batch export: converts every image × every configured size × every
  selected format in one pass, then bundles the full set into a single ZIP
  download

## A detail worth pointing out

Most tools like this stop at `canvas.toBlob()`. This one goes a step
further: `setJpegDpi()` reaches into the raw encoded JPEG bytes after
export to patch in a proper JFIF DPI header — the kind of low-level binary
handling that most canvas-wrapper converters skip entirely.

## Stack

Vanilla HTML/CSS/JS. Canvas API handles all resizing, cropping, and format
conversion. [JSZip](https://stuk.github.io/jszip/) (loaded via CDN) bundles
batch exports into a single download. No build step, no backend, no
dependencies beyond that one script.

## Status

Fully functional, multi-file tool — no setup required beyond opening the
page. Front-end redesign: In progress. Update soon.
