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
- A built-in example scene — a twelve-sided wine glass and a cube — is available from the
  LOAD screen (press `2` then `X`).

Note: browsers block local storage for pages opened via `file://`, so SAVE/LOAD only work
when the page is served over `http://`. Export/import work everywhere.

## Licence

The code in `index.html` is released into the public domain — see `LICENSE`.
