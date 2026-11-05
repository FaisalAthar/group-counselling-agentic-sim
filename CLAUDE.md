# Working on this repository

This is a single-page web app: `index.html` is the whole simulator, served by GitHub Pages from `main`.

## Versioning (do this on every build)

Every change that is pushed counts as a new build:

1. Bump `APP_VERSION` in `index.html` (v1.6 → v1.7 and so on). The page shows it next to the title.
2. Copy the finished `index.html` to `versions/group-circle-sim-<version>.html`, changing the three.js import from `./lib/three.module.min.js` to `../lib/three.module.min.js` so the copy works from that folder. Never edit an older copy.
3. Add a row at the top of the "Versions" table in `README.md` saying what changed, in plain words.

Commit the three together.

## 3D view

The 3D circle is the `<script type="module">` at the end of `index.html`. It only reads app state (`S.members`, `S.rel`, `S.transcript`, the `.speaking` / `.pending` classes) each frame; keep it that way so the 2D fallback keeps working.
