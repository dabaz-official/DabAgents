# 09 — Documentation and Project Memory

**Applies to:** every project. Documentation is part of the deliverable, not an afterthought.

## 1. Required files

| File | Required | Purpose |
|---|---|---|
| `README.md` | yes | What the project is, how to run it, how to deploy it |
| `AGENTS.md` | yes | Project contract: pinned rules, stack, commands, DoD, exceptions |
| `.env.example` | yes, if env vars exist | Variable names and purposes, no values |
| `CHANGELOG.md` | released projects | User-visible changes per version |
| `docs/adr/` | as decisions accumulate | Architecture decision records |

## 2. README template

```md
# Project name

One sentence describing what this is and who it is for.

## Stack

## Quick start

## Scripts

## Environment

## Deployment

## Structure (optional)
```

- Put the fastest path to a running app near the top.
- Keep commands copy-pasteable and current.
- Link to `AGENTS.md` and the design system instead of duplicating them.

## 3. AGENTS.md

- Keep it to one page.
- Pin the versions of DabAgent-Guideline, DabDesign, and DabFonts (tag or commit SHA).
- List the canonical commands and the Definition of Done.
- State the primary locale, the deploy target, and any project-specific rules.
- Record exceptions with a reason and review date.
- Update it when the stack, commands, or scope changes.

Start from [`templates/AGENTS.md`](../templates/AGENTS.md).

## 4. Architecture decision records

Write an ADR when a decision:

- selects a framework, rendering model, or styling system
- changes the data model, authentication, or authorization
- changes deployment, hosting, or infrastructure
- introduces a cross-cutting pattern other work must follow

Format: `docs/adr/NNNN-short-title.md`

```md
# NNNN — Title

- Status: proposed | accepted | superseded by NNNN
- Date: YYYY-MM-DD

## Context

## Decision

## Consequences
```

- ADRs are immutable. Supersede with a new record instead of editing history.
- Link the ADR from the PR that implements it.
- Design decisions belong in DabDesign's governance, not in project ADRs.

## 5. Changelog

- Follow Keep a Changelog; version with semver.
- Sections: Added, Changed, Deprecated, Removed, Fixed, Security.
- User-visible changes only. No internal refactors unless they affect behavior.
- Update the changelog in the PR that ships the change.

## 6. Code comments

- Explain why, not what. The code already says what.
- Delete commented-out code; git remembers it.
- Workarounds include a reason and a removal condition.
- TODOs use `TODO(owner): reason — issue link`.
- Comments, docstrings, and commit messages are in English.

## 7. Documentation rules

- Docs live next to the code they describe.
- Update docs in the same PR as the behavior change.
- Link to the source of truth; never copy token values, font files, or component specs.
- Remove stale documentation instead of leaving it to rot.
- No secrets, internal URLs, or personal data in docs or screenshots.
- Prefer short documents with concrete commands over long prose.

## 8. Decision memory

- Record decisions in an ADR or in DabDesign's governance, not in chat history.
- Read recent ADRs before proposing architecture.
- If a rule is repeatedly waived, amend the rule instead of accumulating exceptions.
- The project's `AGENTS.md` is the entry point; keep it accurate or agents will follow stale instructions.
