# Arena Club Admin — Scan Prototype

Single-file static prototype. No build step, no dependencies.

    public/index.html   the whole app
    vercel.json         static config

## Deploy

**Drag and drop:** zip the `arena-scan-prototype` folder and drop it on
https://vercel.com/new — Vercel serves `public/` automatically.

**CLI:**

    npm i -g vercel
    cd arena-scan-prototype
    vercel          # preview
    vercel --prod   # production

**Git:** push the folder to a repo and import it on Vercel. Framework preset
"Other", build command empty, output directory `public`.

## What's in it

- Home page, Operations › Scan (Scan / Rescan / Hardware tabs), Graders.
- Hardware tab appears only when the Hardware skill is green on the grader page.
- Station setup: one user per station (a user can hold only one), expandable
  device list, click a card for detail, add or remove stations.
- Hardware setup: drag V600 / Fuji / printers between the shelf and stations.
- State lives in the browser's localStorage under the key `ac-admin-proto-v5`.
  Bump that key in the source to reset everyone's saved state after a data change.

## Editing the data

Near the top of the script block:

- `STATIONS` — the station map: scanners and printer per station.
- `SPARE` — hardware sitting on the shelf.
- `ASSIGNED` — device-level user seeds.
- `GRADERS` — the team.
- `hwType()` — naming rules: `Fuji *` is Fuji, `FJ *` is a printer, everything
  else is a V600.
- `stationUsers()` — which user starts on which station.
