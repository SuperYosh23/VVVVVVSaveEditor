
<img width="500" height="200" alt="Untitled drawing (2)" src="https://github.com/user-attachments/assets/4d391a81-d724-45fb-a9bc-6a5ff6bc75d8" />


A single-file HTML tool to view and edit VVVVVV XML saves (.vvv). Upload a save, tweak stats and progress, then export as a .vvv or copy the raw XML.

---

## Features

- **Upload:** Load any XML-formatted VVVVVV save file (.vvv).
- **Parse & display:** Show key stats (time, deaths, flips), location, mode, arrays.
- **Edit controls:** Friendly inputs for trinkets, position, direction, flags, and more.
- **Raw XML editor:** Edit the XML directly, re-parse to sync the UI.
- **Export options:** Download updated XML as `save.vvv` or copy the raw XML to clipboard.

---

## Quick start

1. **Open** https://superyosh23.github.io/VVVVVVSaveEditor/ in your browser (Chrome, Edge, Firefox).
2. **Upload** your `.vvv` save via the “Upload Save” section.
3. **Edit** your fields (e.g., trinkets, position, flags).
4. **Sync** changes using “Sync Form to XML”.
5. **Export** using “Download .vvv” or “Copy raw XML”.

> Tip: You can also paste XML into the Raw XML textbox and click “Parse Raw XML” to load it into the form.

---

## File format notes

- **Save structure:** The editor expects the standard XML structure:
  - **Root:** `<Save><Data>…</Data></Save>`
  - **Counters:** `hours`, `minutes`, `seconds`, `frames`, `deathcounts`, `totalflips`
  - **Location:** `savex`, `savey`, `saverx`, `savery`, `savedir`, `savegc`, `savepoint`
  - **Progress:** `trinkets`, `collect` (array of 0/1), `flags` (array), `crewstats` (array), `worldmap` (array)
  - **Misc:** `summary`, `currentsong`, `teleportscript`, `companion`, `supercrewmate`, `scmprogress`, `finalmode`, `finalstretch`
- **Trinkets vs collect:**
  - **`<trinkets>`** is the numeric count.
  - **`<collect>`** flags which individual trinkets are collected.

---

## Usage details

- **Editing arrays**
  - **CSV format:** Arrays are comma-separated integers, no spaces required.
  - **Sanity checks:** The editor normalizes values to integers when syncing.
- **Raw XML**
  - **Round-trip safe:** Parse from Raw XML, edit via UI, sync back to Raw XML.
  - **Download:** Exports with `.vvv` extension and `text/xml` content type.

---

## Troubleshooting

- **Trinket changes don’t show in-game**
  - **Cause:** `<collect>` array did not match `<trinkets>`.
  - **Fix:** Ensure the first N entries of `<collect>` are `1`.
- **Parse error**
  - **Cause:** Malformed XML or missing `<Data>` node.
  - **Fix:** Verify tags are closed properly. Use “Load Sample” to compare structure.
- **Clipboard blocked**
  - **Cause:** Browser permission.
  - **Fix:** Use “Download .vvv” instead, or grant clipboard permissions.

---

## Limitations

- **Array length validation:** The editor doesn’t enforce exact array lengths for `worldmap`, `flags`, or `crewstats` yet.
- **Song names:** `currentsong` uses numeric indices; mapping to track names isn’t included yet.
- **Room references:** No preset room list or coordinate validation at this time.

---

## Development

- **Single-file:** Pure HTML/CSS/JS, no build step.
- **Parsing:** Uses `DOMParser` and `XMLSerializer`.
- **Export:** Generates a `Blob` with `text/xml` and downloads as `.vvv`.
- **Auto-sync hook:** Listens to `change` on the trinket dropdown and updates `<collect>` and `<trinkets>`.

---

## Tips for power users

- **Direct XML edits:** Tweak the Raw XML, then “Parse Raw XML” to reflect changes in the form.
- **Custom fields:** Missing tags are created on sync, so you can add fields safely.
- **Versioning:** Keep backups of your original `.vvv` before editing.

---

## Disclaimer

- **Back up your saves:** Always keep a copy of your original `.vvv` file before making changes.
- **Compatibility:** Tested with standard VVVVVV XML saves; heavily modded formats may need adjustments.
- **AI generation:** This project is almost entirely AI-generated, including this README.  
- **No affiliation:** I am not associated with the developer of VVVVVV.
