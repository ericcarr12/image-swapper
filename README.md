# Image Swapper

**Live:** https://www.imageswapper.com

A batch image converter that resizes, crops, compresses, and re-encodes
images to JPG, PNG, or WEBP — entirely in the browser. Nothing is uploaded
anywhere; every conversion runs on-device via the Canvas API.

## What it does

- Drag-and-drop or file-picker intake of multiple images at once (up to 20;
  accepts JPG, PNG, WEBP, GIF, and BMP as input)
- An interactive crop tool — a draggable, resizable selection box, fully
  keyboard-operable via arrow keys on each handle — applied per image before
  export. Crop size also shows up as editable Width/Height fields in Image
  Details, kept in sync with the box either way: type an exact pixel size or
  drag a handle, and the other updates to match.
- A quality slider for JPEG/WEBP (PNG always stays lossless)
- Configurable export "rows": define multiple output sizes per image by
  scale factor, fixed width, or fixed height — similar to Figma's
  @1x/@2x/@3x export presets — each with its own filename suffix and choice
  of output format(s)
- A live before/after preview with three view modes — Original, Optimized,
  and a draggable split-screen Compare — modeled on Photoshop's "Save for
  Web," showing the exact file-size delta as quality/size settings change
- Batch export: converts every image × every configured size × every
  selected format in one pass, then bundles the full set into a single ZIP
  download (that option only appears once there's more than one image to
  bundle)
- Share the tool via a copy-link modal, email, or X/Facebook/LinkedIn/
  WhatsApp; a Terms of Use modal covers usage terms
- On narrower screens, the Image Details and Export panels stack above/below
  the preview instead of sitting beside it, and behave as an accordion —
  opening one collapses the other, so exactly one is always visible

## Accessibility

Built to WCAG 2.1 AA: every custom control (crop handles, the compare
slider, collapsible panels) is keyboard-operable with correct ARIA roles
and live values, modals trap focus and hand it back on close, images and
icon-only buttons carry proper alt text/labels, and the layout holds up
at 200% zoom and down to phone-width viewports.

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

Fully functional, single-file tool — no setup required beyond opening the
page.
