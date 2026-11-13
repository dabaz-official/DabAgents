# DabAgent-Guideline

**Version:** 0.4.0 · **Updated:** 2026-11-14

Rules and conventions agents must follow when building and shipping DabAZ web projects.

## Scope

This repository governs how agent-assisted work is planned, written, verified, and shipped. It does not redefine visual design or font assets.

| Source of truth | Entry point | Owns |
|---|---|---|
| [DabDesign](https://github.com/dabaz-official/DabDesign) | [`GUIDELINE.md`](https://github.com/dabaz-official/DabDesign/blob/main/GUIDELINE.md) | Design tokens, components, contrast, motion, voice |
| [DabFonts](https://github.com/dabaz-official/DabFonts) | [`GUIDELINE.md`](https://github.com/dabaz-official/DabFonts/blob/main/GUIDELINE.md) | Font files, typesetting, loading, licensing |
| This repository | `rules/` and `templates/` | Engineering, workflow, quality gates, security, deployment, content/SEO, surface identity, compatibility, documentation |

Start each dependency at its `GUIDELINE.md`. It defines the required read order and routes to the normative files: DabDesign uses `core.md` and `GOVERNANCE.md`; DabFonts uses `TYPESETTING.md`.

Do not copy token values, font files, or component specs into this repository. Link to the source.

**Conflict order:** project `AGENTS.md` → the dependency's `GUIDELINE.md` and its normative files (visual or typographic matters) → this repository.

## Read order

For any web task:

1. The project's `AGENTS.md`
2. [`rules/01-operating.md`](rules/01-operating.md) — the only always-read rule; it routes to the rest.

Read the other rules only when their trigger fires; the table is in rule 01. Do not load all ten by default.

Before UI work, also follow `DabDesign/GUIDELINE.md`. Before typography, punctuation, or font-loading work, follow `DabFonts/GUIDELINE.md`.

## Documents

| # | Document | Covers |
|---|---|---|
| 01 | [Operating Rules](rules/01-operating.md) | Read order and routing, plan-first, ask vs. decide, scope, verification, reporting, stop conditions |
| 02 | [Engineering Standards](rules/02-engineering.md) | Stack selection, structure, TypeScript, styling, components, data, dependencies |
| 03 | [Git and Delivery Workflow](rules/03-workflow.md) | Branches, commits, PRs, reviews, releases, hotfixes |
| 04 | [Quality Gates](rules/04-quality.md) | Canonical scripts, CI, visual/a11y/perf/security gates, testing, Definition of Done |
| 05 | [Security and Privacy](rules/05-security.md) | Secrets, env contract, headers, auth, dependencies, privacy |
| 06 | [Deployment and Operations](rules/06-deployment.md) | Vercel environments, env vars, domains, rollback, observability |
| 07 | [Content, SEO, and i18n](rules/07-content-seo-i18n.md) | Language policy, voice, metadata, structured data, localization |
| 08 | [Compatibility](rules/08-compatibility.md) | Browser matrix, responsive rules, input, progressive enhancement |
| 09 | [Documentation and Memory](rules/09-docs-and-memory.md) | README, AGENTS.md, ADRs, changelog, comments |
| 10 | [Surface Identity](rules/10-surface-identity.md) | Title format, description reuse, icons, Open Graph, manifest, browser colors |

## Adopting in a project

1. Copy [`templates/AGENTS.md`](templates/AGENTS.md) to the project root.
2. Fill in stack, commands, primary locale, and the pinned commit plus `GUIDELINE.md` entry point for DabDesign and DabFonts.
3. Pin this repository to a tag or commit SHA; update deliberately.
4. Add the project's `check` script (see [rule 04](rules/04-quality.md)).
5. Copy [`templates/ci.yml`](templates/ci.yml) to `.github/workflows/ci.yml`.

Until the first tag exists, pin to a commit SHA.

## Changing these rules

- Propose changes via PR and explain the failure the rule prevents.
- Keep rules enforceable. If a rule cannot be checked, make it a principle, not a gate.
- Pre-1.0, breaking changes bump the minor version.
- Visual and design decisions belong in `DabDesign/GUIDELINE.md` and its governance, not here.
- Remove rules that are repeatedly waived instead of accumulating exceptions.

## Repository language

Documentation and code are written in English. Conversation with the user follows the user's language.
