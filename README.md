# Maritime Inn Antigonish — Housekeeping Room Cleaning Log

A single-page web app that replaces the nightly manual spreadsheet for assigning
housekeeping room status. Tap each room's cleaning status, mark any priority
rooms, and generate a print-ready daily log — front page for room assignments,
back page for the daily task and break log — sized to fit on one printed page.

No backend, no build step, no dependencies. It's one static HTML file.

## Features

- **Tap-to-assign** — cycle each room through Full Clean → Stay Clean → Unassigned
- **Priority marking** — flag Full Clean rooms that are booked for the next
  day so housekeeping cleans those first
- **Auto-generated print sheet** — rooms grouped by type, Full Clean and Stay
  Clean sections stacked, sized to print on a single page
- **Static back page** — daily task log and employee break log print
  automatically on page 2 (page 1 front, page 2 back when printed duplex)
- **Notes / Keys** — open space on each page for handwritten notes
- **No login, no database** — everything resets each time you reload; print
  or save as PDF before closing the tab

## Using it

1. Open `room-cleaning.html` in a browser.
2. Tap each room to set it to **Full Clean** (gold) or **Stay Clean** (teal).
   Tap again to clear it.
3. Click **Generate sheet**. If any rooms are Full Clean, you'll land on a
   quick screen to mark **Priority** rooms (booked for tomorrow — clean these
   first). Skips automatically if there are none.
4. Review the generated sheet, then **Print / Save as PDF**. The task/break
   log page is attached automatically as page 2.
5. Use **← Edit assignments** to go back and make changes before printing.

## Running locally

No install needed — it's a static file.

```bash
# just open it
open room-cleaning.html          # macOS
xdg-open room-cleaning.html      # Linux

# or serve it (recommended, avoids local-file browser restrictions)
python3 -m http.server 8000
# then visit http://localhost:8000/room-cleaning.html
```

## Deploying

Since it's a single static file with zero dependencies, any static host works
with no configuration:

**Vercel**
1. Push this repo to GitHub.
2. [vercel.com/new](https://vercel.com/new) → import the repo → Deploy.
   No build command needed.

**GitHub Pages**
1. Repo → Settings → Pages → Deploy from branch → `main` → `/ (root)`.
2. Your app is live at `https://<username>.github.io/<repo-name>/room-cleaning.html`.

**Netlify**
1. [app.netlify.com/drop](https://app.netlify.com/drop) → drag and drop this
   folder. Done.

## Editing the room roster or sizing

Everything lives in one file, `room-cleaning.html`:

- **Room list / types** — `ROOM_TYPES` near the top of the `<script>` section.
- **Table text/row sizing** — `table.roomtable td`, `table.roomtable th` in
  the `<style>` block (see comments — these are tuned to fit one printed page
  and shouldn't need touching unless the room count changes significantly).
- **Notes / Keys box size** — `.notes-box .space` in the `<style>` block.
- **Page margins** — `@page { margin: ... }`.
- **Static task/break log (page 2)** — `buildPage2()` in the `<script>` section.

## Tech

Plain HTML, CSS, and vanilla JavaScript. Fonts: Fraunces, Inter, IBM Plex Mono
(Google Fonts). No frameworks, no build tooling, no npm packages.