# DabAgent-Guideline

**Version:** 0.1.0 · **Updated:** 2026-11-11

Rules and conventions agents must follow when building and shipping DabAZ web projects.

## Scope

This repository governs how agent-assisted work is planned, written, verified, and shipped. It does not redefine visual design or font assets.

| Source of truth | Owns |
|---|---|
| [DabDesign](https://github.com/dabaz-official/DabDesign) | Design tokens, components, contrast, motion, voice |
| `DabFonts` (preferred) or DabDesign `foundation/fonts` (vendored copies) | Font binaries, subsets, loading, licensing |
| This repository | Engineering, workflow, quality gates, security, deployment, content/SEO, compatibility, documentation |

Do not copy token values, font files, or component specs into this repository. Link to the source.

**Conflict order:** project `AGENTS.md` → DabDesign (for visual matters) → this repository.

## Read order

For any web task:

1. The project's `AGENTS.md`
2. `rules/01-agent-operating.md`
3. `rules/02-engineering.md`
4. `rules/03-workflow.md`
5. `rules/04-quality-gates.md`

Then as relevant: `05-security.md`, `06-deployment.md`, `07-content-seo-i18n.md`, `08-compatibility.md`, `09-docs-and-memory.md`.

## Documents

| # | Document | Covers |
|---|---|---|
| 01 | [Agent Operating Rules](rules/01-agent-operating.md) | Plan-first, ask vs. decide, scope, verification, reporting, stop conditions |
| 02 | [Engineering Standards](rules/02-engineering.md) | Stack selection, structure, TypeScript, styling, components, data, dependencies |
| 03 | [Git and Delivery Workflow](rules/03-workflow.md) | Branches, commits, PRs, reviews, releases, hotfixes |
| 04 | [Quality Gates](rules/04-quality-gates.md) | Canonical scripts, CI, visual/a11y/perf/security gates, Definition of Done |
| 05 | [Security and Privacy](rules/05-security.md) | Secrets, env contract, headers, auth, dependencies, privacy |
| 06 | [Deployment and Operations](rules/06-deployment.md) | Vercel environments, env vars, domains, rollback, observability |
| 07 | [Content, SEO, and i18n](rules/07-content-seo-i18n.md) | Language policy, voice, metadata, structured data, localization |
| 08 | [Compatibility](rules/08-compatibility.md) | Browser matrix, responsive rules, input, progressive enhancement |
| 09 | [Documentation and Memory](rules/09-docs-and-memory.md) | README, AGENTS.md, ADRs, changelog, comments |

## Adopting in a project

1. Copy [`templates/AGENTS.md`](templates/AGENTS.md) to the project root.
2. Fill in stack, commands, primary locale, and the pinned design/font versions.
3. Pin this repository to a tag or commit SHA; update deliberately.
4. Add the project's `check` script (see [rule 04](rules/04-quality-gates.md)).

Until the first tag exists, pin to a commit SHA.

## Changing these rules

- Propose changes via PR and explain the failure the rule prevents.
- Keep rules enforceable. If a rule cannot be checked, make it a principle, not a gate.
- Pre-1.0, breaking changes bump the minor version.
- Visual and design decisions belong in DabDesign's governance, not here.
- Remove rules that are repeatedly waived instead of accumulating exceptions.

## Repository language

Documentation and code are written in English. Conversation with the user follows the user's language.
