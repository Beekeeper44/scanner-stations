# Arena Club Admin — Scan & Revault Prototype

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

- Home page. Operations and Vaulting are the working nav menus; the rest are greyed out.
- **Operations › Scan** — Pending Scan with Scan / Rescan / Hardware tabs.
  Clicking a BOXES button opens the scan station: scanner-station picker, per-scanner
  Scan and Load, green sweep animation, card images landing one per second, positions
  you can clear and rescan front or back, and the card table flipping to Pending Grading.
- **Hardware tab** — only when the Hardware skill is green on the grader page.
  Station setup (one user per station, add/remove stations) and Hardware setup
  (drag V600 / Fuji / printers between the shelf and stations).
- **Vaulting › Revault** — only when the Revault skill is green. Scan cards for the
  storage and shipping bin, live QR reading through the camera, bin contents with slot
  ordering, and Revault / Data Issue / Customer Support dialogs. The demo panel
  bottom-left has bins, cards and a reset.
- **Graders** — searchable list, per-grader skill grid; Hardware and Revault gate the
  pages above.

State lives in the browser's localStorage under `ac-admin-proto-v6`. Bump that key in
the source to reset everyone's saved state after a data change.

## Editing the data

Near the top of the script block:

- `STATIONS` — the station map: scanners and printer per station.
- `SPARE` — hardware sitting on the shelf.
- `GRADERS` — the team.
- `hwType()` — naming rules: `Fuji *` is Fuji, `FJ *` is a printer, else V600.
- `stationUsers()` — which user starts on which station.
- `binItems()` — the bin contents list; `RV` inside `cardDialog` — the revault demo cards.

## Camera

The Revault page uses `getUserMedia` plus jsQR to read bin labels. It needs https and
a permission prompt, so it works on the deployed Vercel URL; sandboxed preview frames
usually block it. The Demo buttons cover the same flow without the camera.
