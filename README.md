# VVVVVV Save Editor

A simple browser‑based save editor for [VVVVVV](https://thelettervsixtim.es/).  
This tool lets you upload your `.vvv` save file, view and edit stats, and export the modified save back to `.vvv`.

---

## Features

- **Upload `.vvv` save files** (XML format used by VVVVVV).
- **View and edit stats**:
  - Trinkets (auto‑syncs with `<collect>` array).
  - Death count, flips, time played.
  - Player position (X/Y, room coordinates, direction).
  - Progress flags and arrays (`worldmap`, `flags`, `collect`, `crewstats`).
- **Raw XML editor**: view or paste XML directly.
- **Export options**:
  - Download updated save as `.vvv`.
  - Copy raw XML to clipboard.

---

Usage
Open vvvvvv-save-editor.html in your browser.

Click Upload Save and select your .vvv file.

Edit stats using the form:

Use dropdowns and inputs for trinkets, deaths, flips, etc.

Arrays (worldmap, flags, collect, crewstats) can be edited in textareas.

Click Sync Form to XML to update the raw XML view.

Export:

Download .vvv to save the file.

Or Copy Raw XML and paste into a file manually.

Notes
The editor runs entirely in your browser — no server required.

Always back up your original save before editing.

VVVVVV expects well‑formed XML; malformed edits may cause the game to reject the save.

Currently, trinkets can be set via dropdown. Future versions may add individual checkboxes for each trinket.

License
This project is provided as‑is for personal use. VVVVVV is © Terry Cavanagh. This editor is an unofficial fan tool.

## Trinket Auto‑Sync

VVVVVV tracks trinkets in **two places**:
1. `<trinkets>` — the total count.
2. `<collect>` — a 20‑element array of 0/1 flags for each trinket.

If only `<trinkets>` is changed, the game resets progress.  
This editor automatically updates `<collect>` when you change the trinket dropdown:

- Selecting `N` trinkets sets the first `N` entries in `<collect>` to `1`.
- The rest remain `0`.

Example for 5 trinkets:

```xml
<trinkets>5</trinkets>
<collect>1,1,1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0</collect>


