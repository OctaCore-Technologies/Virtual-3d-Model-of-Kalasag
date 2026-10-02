# KALASAG Node System – Interactive Model

An interactive browser-based model of the KALASAG emergency communication system. It includes a detailed survivor distress node, a conceptual LoRa-to-Wi-Fi relay gateway, and a simulated BDRRMC operations console with an end-to-end acknowledgement flow.

The 3D views include assembled, X-ray, and exploded modes; selectable components; editable distress-node dimensions and appearance; and versioned setup import/export. The relay hardware remains representative until its exact BOM, enclosure, antennas, power design, and backhaul are selected.

## View the model

Open the [deployed GitHub Pages site](https://octacore-technologies.github.io/Virtual-3d-Model-of-Kalasag/).

To run it locally, serve this directory with any static HTTP server and open `index.html`. For example:

```sh
python3 -m http.server 8000
```

Then visit <http://localhost:8000>.

## Repository layout

- `index.html` — self-contained multi-node viewer, relay concept and console simulation
- `kalasag_distress_node_3d.html` — compatibility redirect for the original URL
- `.github/workflows/jekyll-gh-pages.yml` — GitHub Pages deployment workflow
