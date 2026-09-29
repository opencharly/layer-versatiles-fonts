# layer-versatiles-fonts

SDF font glyphs for MapLibre GL JS, bundled locally for the OpenCharly versa
image.

The `versatiles-fonts` candy installs the
[versatiles-org/versatiles-fonts](https://github.com/versatiles-org/versatiles-fonts)
release bundle (`fonts.tar.gz`) into `/opt/versatiles-fonts` as signed-distance-field
PBFs laid out per MapLibre's `{fontstack}/{range}.pbf` glyph-URL convention.
Serving the glyphs locally lets the shortbread MapLibre cell render labels
without hitting `tiles.versatiles.org` as a runtime font CDN. The families
include Fira Sans, Lato, Libre Baskerville, Merriweather Sans, Noto Sans, Nunito,
Open Sans, PT Sans, Roboto, and Source Sans 3.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `versatiles-fonts` |
| Install path | `/opt/versatiles-fonts/` |
| Format | SDF glyph PBFs, `{fontstack}/{range}.pbf` layout |
| Build deps | `curl`, `jq` (arch / fedora) |
| Re-exported at | `/fonts/` by the versatiles-frontend layer |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-versa-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-versatiles-fonts:v2026.243.0410'
```

Then, in a MapLibre client, point the style's glyphs URL at the local bundle:

```javascript
style.glyphs = 'http://127.0.0.1:28002/fonts/{fontstack}/{range}.pbf';
```

The candy's `plan:` asserts the install directory, at least one non-empty `.pbf`,
the default MapLibre family `Noto Sans Regular`, the `0-255.pbf` base range file,
an `agent-check` that a MapLibre client can fetch any family's glyph ranges, and
the `curl`/`jq` packages.

## Layout

- `charly.yml` — the `versatiles-fonts:` candy entity (the `require:`, the
  `curl`/`jq` packages, the download-and-unpack `run:` step, the `check:`
  assertions) and the embedded `versatiles-fonts-skill:` skill entity.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-versa:versatiles-fonts`
- `/charly-versa:versa` — the image composing this layer
- `/charly-versa:versatiles-style` — sibling MapLibre style generator that references this glyph URL pattern
- `/charly-versa:versatiles-frontend` — re-exports this bundle at `/fonts/`
- `/charly-versa:maplibre-versatiles-styler` — UI control that switches between font families
- `/charly-versa:notebook-osm` — the shortbread MapLibre cell that patches `style.glyphs`
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
