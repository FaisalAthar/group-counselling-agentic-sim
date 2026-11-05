# Working on this repository

This is a single-page web app: `index.html` is the whole simulator, served by GitHub Pages from `main`.

## Versioning (do this on every build)

Every change that is pushed counts as a new build:

1. Bump `APP_VERSION` in `index.html` (v1.6 → v1.7 and so on). The page shows it next to the title.
2. Copy the finished `index.html` to `versions/group-circle-sim-<version>.html`. Never edit an older copy.
3. Add a row at the top of the "Versions" table in `README.md` saying what changed, in plain words.

Commit the three together.
