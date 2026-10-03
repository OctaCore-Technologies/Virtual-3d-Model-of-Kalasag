# KALASAG Node System – Interactive Model

A self-contained interactive model of the survivor distress node, a mobile LoRa relay tower on a 4 m telescoping tripod, and an offline incident command console with its physical USB LoRa transceiver.

The relay uses one elevated 5.8 dBi fiberglass antenna, a 3 m low-loss N-to-SMA coax feedline, an ESP32-WROOM-32, SX1262, DS3231 AT24C32 RTC, LM2596 converter and a 12 V 7 Ah field battery. The battery and electronics occupy a low-mounted IP66 weatherproof junction-box concept with sealed cable entries, a mounting plate, battery input and mast clamps. The tower has three folding legs, support braces, rubber feet, telescoping sections and locking collars. There are no relay user-interface controls specified.

The console representation includes ESP32-WROOM-32, SX1262, a 3 dBi magnetic-mount whip, USB cable and small case, 5 V active buzzer and DS3231 AT24C32. Hardware opens as a selectable 3D assembly with a removable case lid, mounting bosses, board standoffs, headers, RF/USB connectors, representative buzzer driver and wiring that follows exploded parts. Switch between **Hardware / Dashboard**; the dashboard explicitly labels all health and incident data as simulated. It supports automatic or operator acknowledgement, response dispatch and reset:

**Survivor node → Mobile relay tower → Console transceiver → Offline console**

## Design requirements and unresolved fit

- The 4 m mast and 5.8 dBi antenna remain requirements. The component sheet's 3.2 m mast and 8 dBi antenna candidates are unresolved.
- The 3 m feedline follows a direct top-gland route. Its external and internal conceptual centerlines are checked against 3 m; purchased connector lengths and installation slack still require confirmation.
- All relay enclosure dimensions and CAD geometry are conceptual until supplier SKUs, battery clearance, cable length/slack, cable glands and mounting hardware are confirmed. IP66 describes the required enclosure, not a tested rating of this visualization.
- The relay represents 915–918 MHz and 18 dBm maximum transmit power. No RF link, electrical circuit or battery runtime is simulated.
- X-ray exposes the enclosure; exploded mode separates its lid, battery and electronics while leaving the deployed tripod intact.
- The component sheet is the source of truth for component selection. The viewer links every component to the sheet and the [local transcription](references/hardware-bom.md). Survivor geometry now shows ADXL345 GY-291, TP5000 set to 3.6 V, an external 5 V adapter, 1/4 W 1% axial resistors and electrolytic capacitors. All three RTC boards include AT24C32 EEPROM detail. Unlisted MCP23017, buck-boost and distribution boards, common button cover and relay fuse are removed.
- One representative IFR18650 3.2 V / 1500 mAh cell and its holder are displayed. The sheet does **not** specify pack quantity or topology; this display is not a one-cell procurement requirement. Non-BOM battery alternatives were removed from the appearance selector.
- TP5000 has IN/BAT terminals, not the previous charger's SYS output. The BOM does not resolve regulated load supply, simultaneous charging/load behavior, GPIO allocation for all buttons/LEDs, or passive values. These unresolved connections are omitted instead of inventing extra hardware. I²C/SPI, RF and charger/BMS wiring remain conceptual; this is not a fabrication schematic.
- [The original component audit](references/component-model-audit.md) and transcription comparisons are preserved as the `10806ec` baseline. [The alignment record](references/sheet-alignment.md) describes current changes and remaining sheet conflicts.

## Test locally

Open `index.html` directly in a desktop browser. The embedded Three.js library needs no build step or network connection. Do not use GitHub Pages as the test environment.

The Relay tab opens centered on the field enclosure. Select **Enclosure**, **Antenna** or **Full tower** for smooth framing transitions. Orbit and zoom remain centered on the selected focus. Pan vertically with Shift-drag, right-drag, Shift-scroll, the **Mast height** slider, or two-finger drag; pinch to zoom on touch devices. Heights use the conceptual 7 display units per metre scale, including the antenna above the 4 m mast. Reset restores enclosure focus, default orbit and framing, and stops auto-rotation. Switching tabs preserves camera focus, orbit, zoom and pan; resizing preserves relative zoom. Relay and console wiring follow their module terminals in exploded mode.

Check all three tabs, each relay focus preset, vertical panning, orbit and zoom, all ten selectable relay parts, labels, X-ray and exploded modes. Inspect all seven console hardware components. In Dashboard, send a test alert, inspect Spatial ID, location, severity and local timestamps, acknowledge or wait for automatic acknowledgement, dispatch a response, and reset. Reset cancels pending alert timers; automatic acknowledgement cannot regress an operator dispatch. Inspect the distress-node DS3231 RTC and its four wires (VCC, GND, SDA, SCL), ADXL345, TP5000, passives and external adapter. Repeat at a mobile viewport and check the browser console for JavaScript errors.

If your browser restricts local files, serve this directory locally:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Then open `http://127.0.0.1:8000/index.html#relay`. Keep testing local; review the result before committing or pushing. Do not push to `main` without approval.

## Repeatable browser verification

With the local server running and Playwright available to Node, run:

```sh
MODEL_URL=http://127.0.0.1:8000/index.html node tests/browser-check.cjs
```

The checks use Chromium with WebGL software rendering, desktop and mobile viewports, real mouse/touch input, hardware selection, X-ray, exploded-wire endpoints, incident acknowledgement/dispatch/reset, tab persistence and browser error capture. Set `ARTIFACT_DIR` to a local directory to save inspection screenshots. Playwright is a test dependency only; the viewer itself remains offline and self-contained.

## Sources

The KALASAG Proposal, §6, provides system context. Component selection is governed by the [component sheet](https://docs.google.com/spreadsheets/d/1QLaJ-uK42XSZoBPESpl_FkiHE4a3wLdfT5JuzkQpVLM/edit?gid=0). A [local Markdown snapshot](references/hardware-bom.md) preserves the sheet’s BOM, candidate notes and supplier links, with local comparison markers linked to the [component audit](references/component-model-audit.md). The supplied mast image is a tripod-form reference only; its lights and crossbar are excluded.

## Repository layout

- `index.html` — embedded 3D viewer, relay tower, console hardware assembly and dashboard simulation
- `kalasag_distress_node_3d.html` — compatibility redirect for the original URL
- `tests/browser-check.cjs` — local Chromium interaction and rendering regression checks
