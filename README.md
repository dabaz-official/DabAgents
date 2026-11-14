# DabAgents

**Version:** 1.0.0 · **Updated:** 2026-11-14

Rules and conventions agents must follow when building and shipping DabAZ web projects.

## Scope

This repository governs how agent-assisted work is planned, written, verified, and shipped. It does not redefine visual design or font assets.

| Source of truth | Entry point | Owns |
|---|---|---|
| [DabDesign](https://github.com/dabaz-official/DabDesign) | [`GUIDELINE.md`](https://github.com/dabaz-official/DabDesign/blob/main/GUIDELINE.md) | Design tokens, components, contrast, motion |
| [DabFonts](https://github.com/dabaz-official/DabFonts) | [`GUIDELINE.md`](https://github.com/dabaz-official/DabFonts/blob/main/GUIDELINE.md) | Font files, typesetting, loading, licensing |
| This repository | `rules/` and `templates/` | Engineering, workflow, quality gates, security, deployment, content, surface identity, compatibility, documentation |

Start each dependency at its `GUIDELINE.md`. It defines the required read order and routes to the normative files: DabDesign uses `core.md` and `GOVERNANCE.md`; DabFonts uses `TYPESETTING.md`.

Do not copy token values, font files, or component specs into this repository. Link to the source.

**Conflict order:** project `AGENTS.md` → the dependency's `GUIDELINE.md` and its normative files (visual or typographic matters) → this repository.

## Read order

For any web task:

1. The project's `AGENTS.md`
2. [`rules/01-operating.md`](rules/01-operating.md) — the only always-read rule; it routes to the rest.

Read another rule only when its trigger fires. Do not load all ten by default.

Before UI work, follow `DabDesign/GUIDELINE.md`. Before typography, punctuation, or font-loading work, follow `DabFonts/GUIDELINE.md`.

## Documents

| # | Document | Covers |
|---|---|---|
| 01 | [Operating Rules](rules/01-operating.md) | Task loop, ask vs. decide, scope, verification, routing, stop conditions |
| 02 | [Engineering Standards](rules/02-engineering.md) | Stack selection, structure, TypeScript, styling, components, data, dependencies |
| 03 | [Workflow](rules/03-workflow.md) | Branches, commits, PRs, reviews, releases, hotfixes |
| 04 | [Quality Gates](rules/04-quality.md) | Canonical scripts, CI, visual/a11y/perf gates, testing, Definition of Done |
| 05 | [Security and Privacy](rules/05-security.md) | Secrets, env contract, headers, auth, dependencies, privacy |
| 06 | [Deployment](rules/06-deployment.md) | Vercel environments, env vars, domains, rollback, observability |
| 07 | [Content, SEO, and i18n](rules/07-content.md) | Language policy, voice, SEO, localization, media, content structure |
| 08 | [Compatibility](rules/08-compatibility.md) | Browser matrix, responsive rules, input, progressive enhancement |
| 09 | [Documentation](rules/09-docs.md) | README, AGENTS.md, ADRs, changelog, comments |
| 10 | [Surface Identity](rules/10-surface-identity.md) | Title format, description reuse, icons, Open Graph, manifest, browser colors |

## Templates

Copy these into a project. They are assets, not rules to read on every task.

| Template | Copy to | Purpose |
|---|---|---|
| [`AGENTS.md`](templates/AGENTS.md) | project root | Project contract: pins, stack, commands, DoD, surface assets, exceptions |
| [`README.md`](templates/README.md) | project root | README skeleton: quick start, scripts, environment, deployment |
| [`adr.md`](templates/adr.md) | `docs/adr/NNNN-short-title.md` | ADR format |
| [`ci.yml`](templates/ci.yml) | `.github/workflows/ci.yml` | CI that runs `pnpm check` |
| [`og-image.md`](templates/og-image.md) | reference for the OG generator | Layout for generated 1200×630 images |

## Adopting in a project

1. Copy `templates/AGENTS.md` to the project root; fill in identity, stack, commands, locale, and canonical URL.
2. Fill in `Surface assets`: plate and mark master paths (rule 10 §4), and whether the home OG image is custom or generated.
3. Pin this repository, DabDesign, and DabFonts by tag or commit SHA. Until `v1.0.0` is tagged, pin a commit SHA.
4. Copy `templates/README.md` and `templates/ci.yml`; add the `check` script (rule 04).
5. Use `templates/adr.md` for the first decision that needs a record.

## Versioning and changes

- Semantic versioning; tag releases `vX.Y.Z`.
- Breaking rule changes bump the major version. Projects pin and upgrade deliberately.
- `CHANGELOG.md` records user-visible changes; read it before upgrading a pin.
- Propose changes via PR and explain the failure the rule prevents.
- Keep one canonical home per rule; link instead of restating.
- Visual and design decisions belong in `DabDesign/GUIDELINE.md` and its governance, not here.

## Repository language

Documentation and code are written in English. Conversation with the user follows the user's language.

## License

Released under the MIT license, © 2026 DabAZ; see [`LICENSE`](LICENSE).
The rules, the templates, and this documentation are covered. Copy
`templates/` into a project freely, with or without attribution.
