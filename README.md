# ETS2 Route Advisor — a live GPS dashboard for Euro Truck Simulator 2

A single-file, self-contained GPS-style dashboard for **Euro Truck Simulator 2**, built to run on a second monitor while you drive. It reads live telemetry from your game and shows your position, heading, speed, fuel, and rest timer on top of a real map — plus a 3D truck marker, your full driven-route trail, and a couple of extras like a Last.fm "now playing" card.

> **Unofficial fan project.** Not made by, affiliated with, or endorsed by SCS Software. "Euro Truck Simulator 2" and "ETS2" are trademarks of SCS Software.

## Features

- **Live position on a real map** — your truck's position, heading, and driven trail rendered over a calibrated map image, with a full-map "Overview" mode and a close-up driving view
- **3D truck marker** — a generic low-poly rig (not an in-game asset) that rotates to match your real heading, in your choice of size and color
- **Speed, fuel, and rest math** — current speed vs. speed limit, fuel remaining in liters *and* estimated range in km, and estimated distance you'll cover before your next mandatory rest stop
- **Per-job trail segments** — driven roads stay on the map job after job, without a stray line connecting one job's endpoint to the next job's start
- **Map calibration tool** — load your own map screenshot and calibrate it by clicking a few cities and entering their real in-game coordinates
- **Export / Import** — back up your entire driven trail to a `.json` file and load it back in later, so your history survives closing the tab
- **Last.fm "Now Playing"** — optional card showing your currently playing track
- **Demo Mode** — try the whole dashboard with simulated data before hooking up the game

## Requirements

- **Euro Truck Simulator 2** (or American Truck Simulator)
- **[ETS2 Telemetry Server](https://github.com/Funbit/ets2-telemetry-server)** by Funbit — a free, open-source background app that reads the game's telemetry and serves it locally. This dashboard talks to it, it doesn't replace it.
- Any modern desktop browser

## Getting started

1. Install and run the **ETS2 Telemetry Server**, then launch ETS2 and click **Drive** on a job (telemetry only streams once you're actually driving).
2. Download `ets2-gps.html` from this repo.
3. **Important — avoiding a CORS error:** browsers block a plain local file from reading `localhost:25555` directly. The fix is to serve the dashboard from the telemetry server itself instead of opening it as a bare file:
   - Find your telemetry server's install folder, then the subfolder `server\Html\skins\`
   - Create a new folder there (e.g. `routeadvisor`) and copy `ets2-gps.html` into it
   - Open **`http://localhost:25555/skins/routeadvisor/ets2-gps.html`** in your browser instead of double-clicking the file
4. Drag that tab to your second monitor and hit the **Fullscreen** button (or press `F`).

> Because this fix relies on the dashboard and the telemetry API sharing the same local origin, the **hosted version of this page (e.g. GitHub Pages) can't read your local telemetry server directly** — you'll hit the same CORS error. For live data, use the downloaded copy via the skins-folder method above; the hosted version is best for browsing the code, trying Demo Mode, or as a starting point to download from.

## Calibrating your own map

The dashboard ships with a pre-calibrated default map. To use your own screenshot instead:

1. Click **Load Map Image** and pick your image (a map with visible city labels works best)
2. In the calibration panel, click a city, then enter its real in-game X / Z coordinate (a built-in reference table has values for common cities)
3. Repeat for **3 or more points**, spread as far apart as possible, then **Save calibration**

## Optional: Last.fm Now Playing

1. Get a free API key at [last.fm/api/account/create](https://www.last.fm/api/account/create)
2. Open **Settings** and enter your Last.fm username and API key

## Backing up your history

Click **Export** any time to download your full driven trail as a `.json` file. Click **Import** to load a previous export back in (this replaces whatever trail is currently on screen, so it'll ask you to confirm).

## Known limitations

- The 3D truck is a generic stylized rig, not a model of your actual truck — SCS Software's in-game truck models are copyrighted and aren't reproduced here
- Map calibration is accurate to roughly 1–3 km on a map spanning well over 1,000 km — good enough to place you on the right road, not survey-grade
- Zooming in past the map image's native resolution shows crisp pixels rather than more real detail — there's a hard limit to any fixed image
- The rest-stop distance estimate is based on your recent average speed, so it's a smoothed estimate, not an exact figure

## Credits

- [ETS2 Telemetry Server](https://github.com/Funbit/ets2-telemetry-server) by Funbit — the telemetry source this dashboard depends on
- City coordinate reference data adapted from [ETS2-City-Coordinate-Retriever](https://github.com/Koenvh1/ETS2-City-Coordinate-Retriever) by Koenvh1
- [three.js](https://threejs.org/) for the 3D truck marker
- Built with the help of [Claude](https://claude.ai) (Anthropic)

## License

[MIT](LICENSE) — do what you like with it, just don't hold me liable if your truck's engine wear hits 100%.
