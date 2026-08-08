# VU-3D — web edition

A dependency-free, single-file re-imagining of **VU-3D** (Psion, 1982) for the ZX Spectrum:
the 3D design program where you build a solid by drawing stacked 2D cross-sections ("Z
planes"), then orbit it and render it as wire line, hidden line, or shaded solid.

Open `index.html` in a browser. That's it — no build step, no dependencies, no network
requests.

## What it does

- **CREATE / OPEN** — draw a slice with `O`pen, `S`tart, `L`ine, `D`elete, `E`nd; then
  `F`igure, `M`agnify, `R`educe, arrows to shift, `N`ext z, `C`lose, `Q`uit. As in the
  original, a figure's lines may never cross and two figures may never intersect — but one
  figure may sit inside another to make a hole.
- **MODIFY** — walk the existing Z planes and adjust them.
- **DISPLAY / PICTURE** — orbit the "observing sphere" with the arrows, `N`ear / `F`ar,
  `M`agnify / `R`educe; render as wire line, `H`idden line, or `S`hade (light above /
  centre / below × left / centre / right, then grey or pattern).
- **COLOUR**, **SAVE**, **LOAD**, **ABANDON** — as on the original main menu.

`CAPS SHIFT` is mapped to `Shift` for fine movement, and `5 6 7 8` still work as cursor keys.

## Where it differs from 1982

- 3D is rendered with **WebGL 2** instead of CPU dithering. Grayscale shading is a smooth
  diffuse ramp; patterned shading thresholds the same lighting against an 8×8 Bayer matrix
  in *logical* pixels, so it keeps the chunky look of the original at any zoom.
- Press `T` to flip between the authentic 256×192 screen and high-resolution rendering.
- Banner commands are clickable, and the mouse places points in OPEN and drags the view in
  DISPLAY.
- Cassette SAVE / LOAD become named browser-storage slots, plus `.json` export/import;
  `K`eep saves a PNG instead of a `SCREEN$`; `P`rint opens the browser print dialogue.
- The built-in example (press `2` then `X`) is Psion's own EXAMPLE scene — a wine glass and
  a cube — recovered from the memory image in `VU-3D/VU3DEXMP.TAP`. See below.

## The EXAMPLE data file

The two tapes carry byte-identical code blocks; the example differs only in its BASIC loader
(`LET ab=1` — a data file is present — and `GO TO 370` to skip the opening question). The
data file itself is still sitting in the saved memory image:

- **vertex table at 32814** — 108 vertices, each `(x, y, z)` as three signed little-endian
  words, grouped into rings of constant `z` (one ring per figure per Z plane);
- **face list at 61280** — a count (91) followed by `[n][v0..vn-1]` records: one 12-sided
  cap and 90 quads.

Decoded, it is a 12-sided wine glass on eight Z planes (foot capped, rim left open) plus a
cube on two planes — matching the manual's suggestion to "examine the glass ... using the
MODIFY option". The original Z axis runs downward, so it is flipped to stand the glass on
its foot and scaled by 0.864 to fit the workspace; the data is otherwise unaltered and is
embedded in `index.html` as `EXAMPLE_FIGS`.

Note: browsers block local storage for pages opened via `file://`, so SAVE/LOAD only work
when the page is served over `http://`. Export/import work everywhere.

## Reference material

This project was built against the original tape images (`VU3DPUR.TAP`, `VU3DEXMP.TAP`), the
tape inlay text, the Timex/Sinclair manual and a screenshot of the CREATE screen. Those sit
in a local `VU-3D/` directory which is **git-ignored and not distributed** — they are still
under copyright. Nothing in the app reads them at runtime; the `.tap` files were only
inspected (and can be run in an emulator such as `fuse`).

## Licence

The code in `index.html` is released into the public domain — see `LICENSE`. VU-3D itself is
© Psion Ltd 1982 and its manual © Timex Computer Corporation 1983; the geometry of the
built-in example derives from Psion's EXAMPLE tape.
