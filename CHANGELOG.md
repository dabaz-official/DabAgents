# Changelog

All notable changes to this repository are recorded here. The format follows Keep a Changelog; versions follow semantic versioning.

## 1.0.2 — 2026-11-15

### Fixed

- Rule 04 §3 and `templates/ci.yml` state the npm path and the Node version
  input correctly: the shared workflow installs with pnpm only and defaults to
  Node 24, so npm projects keep a local workflow and other Node LTS versions are
  passed explicitly.
- The 1.0.1 changelog had two `### Changed` headings; they are merged.

## 1.0.1 — 2026-11-15

### Added

- `LICENSE`: the MIT license, and a README license section. A project that pins
  these rules can now reuse them and point at a license.
- Rule 03 §5: version numbers are per repository, and each repository defines
  what a breaking change means in its `AGENTS.md`.
- `AGENTS.md` Versioning: what major, minor, and patch mean for this repository
  (rule 03 §5).

### Changed

- `templates/ci.yml` calls the shared `web-ci.yml` from `dabaz-official/.github`
  instead of copying its steps. The gate is the project's `pnpm check`, so the
  workflow definition and the gate definition are no longer two documents.
- Rule 04 §3 points at that shared workflow and names `pnpm check` as the only
  thing CI restates.
- Adoption pins by tag, with a commit SHA only where a repository has no tag.
- Rule 09 §3 names the entry point per dependency: `rules/01-operating.md` for
  DabAgents, `GUIDELINE.md` for DabDesign and DabFonts.
- `templates/AGENTS.md` accepts a tag or a commit SHA for all three pins, adds
  320 px to the responsive check, and restates the full Definition of Done from
  rule 04 §8, including the accessibility, performance, and preview-deploy gates.

### Fixed

- Rule 02 §6 points at the archived component drafts under `archive/`; DabDesign
  no longer has a live `components/` directory.
- README no longer says templates may be copied without attribution, which the
  MIT license does not allow for substantial copies.

## 1.0.0 — 2026-11-15

The guideline set was rewritten around one always-read rule, trigger-based loading, and one canonical home per rule.

### Added

- `rules/01-operating.md` as the only always-read rule, with the trigger table that routes to rules 02–10.
- `templates/README.md` as the project README skeleton.
- `templates/adr.md` as the ADR format.
- `templates/AGENTS.md` `Surface assets` section: plate and mark master paths, and whether the home OG image is custom or generated.
- `rules/04-quality.md` testing strategy: what to test with Vitest, React Testing Library, and Playwright, and what not to test.
- `CHANGELOG.md`.

### Changed

- Each rule now has one canonical home. The Definition of Done lives in rule 04, viewports in rule 08, security in rule 05, metadata in rule 10, and templates in `templates/`.
- Rule 03 review checklist points to the Definition of Done instead of restating it.
- Rule 04 points to `templates/ci.yml`; the CI workflow is no longer embedded in the rule.
- Rule 09 points to `templates/README.md` and `templates/adr.md`; the templates are no longer embedded in the rule.
- Rule 07 owns voice and microcopy. DabDesign is described as visual only; it no longer owns tone.
- Rule 10 supports one or two icon masters: a plate master for iOS and maskable, and a transparent mark master for `favicon.ico`, `icon.svg`, `icon-192.png`, and `icon-512.png`. Supplied alpha is preserved; transparent corners are never filled, padded, or re-rounded.
- Rule 10 uses a supplied home OG image as-is and generates one only when it is absent. The generated home fallback uses the site name as title and the tagline as the supporting line; the wordmark is omitted.
- Short filenames: `01-operating.md`, `04-quality.md`, `07-content.md`, and `09-docs.md`.
- `README.md` rewritten for 1.0.0: source of truth, read order, documents, templates, adoption, and versioning.

### Removed

- Duplicated review checklists from rule 03 and duplicated gate details from rule 04.
- Inline README and ADR templates from rule 09.
- Voice ownership from the DabDesign description in this repository.
- Old filenames: `01-agent-operating.md`, `04-quality-gates.md`, `07-content-seo-i18n.md`, and `09-docs-and-memory.md`.

## Pre-1.0

Known milestones before this changelog existed:

- **0.4.0 — 2026-11-14** — Added rule 10 Surface Identity; home title is site-name-first; icons may use baked corners within the platform mask and alpha outside the plate; the maskable plate covers the central 80% circle.
- **0.3.0 — 2026-11-12** — Introduced the layered read order: rule 01 is the only always-read rule and routes to the rest by trigger; removed duplicated checklists.
- **0.1.1 — 2026-11-12** — Wired the DabDesign and DabFonts `GUIDELINE.md` entry points; aligned component, viewport, and font rules.
- **0.1.0 — 2026-11-11** — Initial rules 01–09, `templates/AGENTS.md`, CI workflow, and OG image layout.
