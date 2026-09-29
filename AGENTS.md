# AGENTS.md — layer-versatiles-fonts

Standalone candy repo for the `versatiles-fonts` layer — the local SDF font
glyph bundle for MapLibre GL JS in the versa image. The candy lives in
`charly.yml` at the repo root: the `require:` on `layer-supervisord`, the
`curl`/`jq` packages, the download-and-unpack `run:` step, the `check:`
assertions, and the embedded `skill:` entity projected into the marketplace
corpus as `/charly-versa:versatiles-fonts`.

Canonical files:

- `charly.yml` — the `versatiles-fonts:` candy entity and the
  `versatiles-fonts-skill:` skill entity.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-versa:versatiles-fonts` — the owning skill. The glyph-URL layout, the
  families, and the re-export at `/fonts/`. Load before editing or troubleshooting
  the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:` and `agent-check:`, per-distro `distro:`
  arms, package/repo sections, service declarations). Load before editing any
  entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence. The
  `Noto Sans Regular` and `0-255.pbf` checks guard against a partial tarball.
- The install resolves the `fonts.tar.gz` asset from the GitHub API by exact
  filename; a release-layout change must update that selector.

## Modify this repo

- Edit the `versatiles-fonts:` candy entity AND the `versatiles-fonts-skill:`
  skill entity in `charly.yml` together. The skill is the projected usage source,
  so a behaviour change not mirrored in the skill leaves the corpus stale.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge on
  PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the PR
  body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
