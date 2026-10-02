# KALASAG Node System – Interactive Model

A self-contained interactive model of the survivor distress node, a mobile LoRa relay tower on a 4 m telescoping tripod, and an offline incident command console with its physical USB LoRa transceiver.

The relay uses one elevated 5.8 dBi fiberglass antenna, a 3 m low-loss N-to-SMA coax feedline, an ESP32-WROOM-32, SX1262, DS3231 RTC, LM2596 converter and a 12 V 7 Ah field battery. The battery and electronics occupy a low-mounted IP66 weatherproof junction-box concept with sealed cable entries, a mounting plate, fused input and mast clamps. The tower has three folding legs, support braces, rubber feet, telescoping sections and locking collars. There are no relay user-interface controls specified.

The console representation includes ESP32-WROOM-32, SX1262, a 3 dBi magnetic-mount whip, USB cable and small case, 5 V active buzzer and DS3231. The existing dashboard simulates acknowledgement and response dispatch:

**Survivor node → Mobile relay tower → Console transceiver → Offline console**

## Design requirements and unresolved fit

- The 4 m mast and 5.8 dBi antenna remain requirements. The component sheet's 3.2 m mast and 8 dBi antenna candidates are unresolved.
- The 3 m feedline may be insufficient at full mast extension with the enclosure mounted low; verify the deployed route and slack before selecting the cable.
- All relay enclosure dimensions and CAD geometry are conceptual until supplier SKUs, battery clearance, cable length/slack, cable glands and mounting hardware are confirmed. IP66 describes the required enclosure, not a tested rating of this visualization.
- The relay represents 915–918 MHz and 18 dBm maximum transmit power. No RF link, electrical circuit or battery runtime is simulated.
- X-ray exposes the enclosure; exploded mode separates its lid, battery and electronics while leaving the deployed tripod intact.
- The distress node includes a selectable DS3231 RTC on the existing 3.3 V I²C bus; its power design is preserved. Proposal/sheet differences with the later design (SW-420 versus ADXL345, single IFR18650 versus 1S2P, TP5000 versus BQ25185, and added MCP23017/TPS63070) need a source-of-truth decision before changes.

## Test locally

Open `index.html` directly in a desktop browser. The embedded Three.js library needs no build step or network connection. Do not use GitHub Pages as the test environment.

The Relay tab opens centered on the field enclosure. Use **Full tower** to frame the deployed mast and **Focus enclosure** to return. Relay wiring follows the module terminals in exploded mode.

Check all three tabs, the initially centered enclosure and full-tower toggle, orbit and zoom, all ten selectable relay parts, labels, X-ray and exploded modes. Select each console hardware item, send a test alert, wait for acknowledgement, dispatch a response, and reset. Inspect the distress-node DS3231 RTC and its four wires (VCC, GND, SDA, SCL). Repeat at a mobile viewport and check the browser console for JavaScript errors.

If your browser restricts local files, serve this directory locally:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Then open `http://127.0.0.1:8000/index.html#relay`. Keep testing local; review the result before committing or pushing. Do not push to `main` without approval.

## Sources

The hardware follows the KALASAG Proposal, §6, and the [component sheet](https://docs.google.com/spreadsheets/d/1QLaJ-uK42XSZoBPESpl_FkiHE4a3wLdfT5JuzkQpVLM/edit?gid=0). The supplied mast image is a tripod-form reference only; its lights and crossbar are excluded.

## Repository layout

- `index.html` — embedded 3D viewer, relay tower, console hardware illustration and dashboard simulation
- `kalasag_distress_node_3d.html` — compatibility redirect for the original URL
