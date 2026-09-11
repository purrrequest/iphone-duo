# iPhone Duo · Seated Fold Preview

A browser-based study of the Apple iPhone Duo, forked from [chuspeeism/iphone-duo](https://github.com/chuspeeism/iphone-duo) (MIT). Instead of the upstream demo's fully-open "book" layout (hinge upright, unfolding left-right), this build rolls the device 90° so its hinge sits at the bottom — like a laptop opened on a desk — and lets you swap in your own image on both screens.

The Apple model only ships two baked poses in its USD "Pose" variant set (`Closed`, `Landscape`); there's no separate "seated" or "laptop" geometry. This pose is produced client-side from that same base mesh by rolling the whole device 90° and repositioning the camera. The fold geometry is unchanged from upstream; the screen shader's blur/darken calibration has been retuned for this closer camera framing, and custom image uploads are cropped separately for the inner and outer screens (they're different shapes, so a single stretched crop doesn't fit both).

## Run locally

Static HTML/CSS/JS, no build step. Three.js is bundled in `vendor/`.

The Apple reference assets are prepared separately (Python 3.12+):

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install usd-core
python scripts/prepare-assets.py
python -m http.server 8766 --bind 127.0.0.1
```

Open `http://127.0.0.1:8766/`. The prepared files land in the ignored `assets/` directory.

## Using it

- The slider folds and unfolds the device, from fully closed to fully open.
- **Fold / Unfold** jumps between closed and the Seated pose.
- **Screen UI → Custom** opens an image picker and applies your image to both screens (kept local to your tab — nothing is uploaded anywhere).
- Drag to orbit, scroll to zoom.
- The sun/moon button in the top corner switches between light and dark themes (remembered on your next visit; otherwise follows your system setting).

## Source map

| File | Purpose |
| --- | --- |
| `index.html` | Screen-UI tabs, fold slider, theme toggle |
| `main.js` | Three.js scene, fold deformation, device roll, projected UI (separately cropped for the inner and outer screens), blur/darkening |
| `ui.js` | Default screen layouts |
| `style.css` | Layout and light/dark theme tokens |
| `scripts/prepare-assets.py` | Download and prepare the reference assets |

## License and sources

Original and modified application code is released under the MIT license (see `LICENSE`), carrying forward the upstream project's license.

Apple's model, embedded model textures, and screen imagery are excluded from the repository and the MIT license; `scripts/prepare-assets.py` links to their original sources and their use is subject to Apple's terms. This project is an independent animation study, not an Apple product.

- [Apple iPhone Duo](https://www.apple.com/iphone-duo/)
- [Apple HIG: Designing for iPhone Duo](https://developer.apple.com/design/human-interface-guidelines/designing-for-iphone-duo)
- [Three.js](https://threejs.org/)
- Forked from [chuspeeism/iphone-duo](https://github.com/chuspeeism/iphone-duo)
