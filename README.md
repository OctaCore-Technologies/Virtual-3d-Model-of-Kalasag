# KALASAG Distress Node – Interactive 3D Model

An interactive browser-based model of the KALASAG survivor distress node. The viewer includes assembled, X-ray, and exploded views; selectable components; editable component dimensions and appearance; and setup import/export.

## View the model

Open the [deployed GitHub Pages site](https://octacore-technologies.github.io/Virtual-3d-Model-of-Kalasag/).

To run it locally, serve this directory with any static HTTP server and open `index.html`. For example:

```sh
python3 -m http.server 8000
```

Then visit <http://localhost:8000>.

## Repository layout

- `index.html` — self-contained viewer and 3D model
- `kalasag_distress_node_3d.html` — compatibility redirect for the original URL
- `.github/workflows/jekyll-gh-pages.yml` — GitHub Pages deployment workflow
