# Wasp Companion

Single-file Web Bluetooth companion for wasp-os watches (built for the Colmi P8). No build step, no backend.

## Run
- Locally: `python3 -m http.server 8000` then open http://localhost:8000 in Chrome/Edge (Web Bluetooth needs https or localhost).
- GitHub Pages: push `index.html` to a repo, Settings > Pages > deploy from branch. Open the https URL in Chrome/Edge on desktop or Android. iOS needs the Bluefy browser.
- No watch handy: press **Demo** (simulated watch using the same BLE/REPL code path).
- Self-test (headless): `index.html?selftest` runs the protocol checks against the simulated watch and writes PASS/FAIL into `<pre id="selftest">`.

## Features
Time sync, battery/RAM/flash, buzz, reboot; step history from `logs/YYYY/MM-DD.steps` (day/week/month/all charts, goal, CSV, cached in IndexedDB); notifications; weather push (Open-Meteo); music display text; watch-face switcher; app install (+ register at boot via main.py); file browser/upload/download/delete; raw REPL console.

## How it talks to the watch
Nordic UART Service over BLE. Each operation: Ctrl-C to stop the watch, send `print('@@'+'B');exec('<code>');print('@@'+'E')`, parse the output between the markers, then `wasp.system.run()` + Ctrl-X ~5 s later to resume (same sequence as `tools/wasptool`).

## Status
Tested only against the built-in simulated watch. Real P8 behaviour (advertised name, write mode, MTU, speed) still to verify.
