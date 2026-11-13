# 03 — Workflow

**Applies to:** every repository. `main` is always deployable.

## 1. Branching

- Work trunk-based: short-lived branches from `main`, merged back quickly.
- Branch names: `feat/<slug>`, `fix/<slug>`, `chore/<slug>`, `docs/<slug>`, `refactor/<slug>`.
- Keep a branch alive for less than three days. Split large work instead.
- Solo exception: documentation, typo, and one-line fixes may go directly to `main`. Anything touching behavior uses a branch.

## 2. Commits

Use Conventional Commits: `type(scope): imperative summary`.

- Types: `feat`, `fix`, `refactor`, `perf`, `docs`, `test`, `build`, `ci`, `chore`, `revert`.
- Summary: imperative, lowercase, no trailing period, ≤72 characters.
- One logical change per commit. Never mix formatting with behavior.
- Body explains the reason and any tradeoff. Reference issues when they exist.
- Commit only files changed for the task.

Examples: `feat(resume): add print stylesheet`, `fix(nav): restore focus after dialog close`.

## 3. Pull requests

Open a PR when the change:

- adds a feature or changes user-visible behavior
- adds or upgrades a dependency
- changes schema, auth, deployment, or infrastructure
- touches more than three files or roughly 200 lines

Skip the PR only for the solo exception above.

A PR description contains:

- **What** changed and **why**
- **How** it was verified (commands, screenshots, preview URL)
- **Risk** and rollback notes
- Screenshots or a short recording for every UI change

Keep PRs under ~400 changed lines when practical. Self-review the diff before asking for review. Squash merge and delete the branch.

## 4. Review and merge

- The PR must satisfy the Definition of Done in [rule 04 §8](04-quality-gates.md). Do not merge with a failing gate.
- The diff stays within the stated scope; unrelated changes are split out.
- UI changes include screenshots or a preview link.
- Risks and rollback notes are in the PR.
- If a gate is waived, record the exception in the project's `AGENTS.md` (rule 04 §9).

## 5. Releases and versioning

- Use semantic versioning: `MAJOR.MINOR.PATCH`.
- Tag production releases: `vX.Y.Z`.
- Maintain `CHANGELOG.md` for released projects; user-visible changes only.
- Breaking changes require a major bump and a migration note.
- Release from `main` only.
- Do not move or reuse a published tag.

## 6. Hotfixes

- Branch from `main`, make the smallest safe fix, open a PR, deploy, tag a patch release.
- Do not bundle unrelated changes into a hotfix.
- If the process failed, add a short root-cause note to the PR or an ADR.

## 7. Never do

- force-push `main` or a shared branch
- rewrite published history
- commit `.env`, keys, tokens, or credentials
- commit commented-out code or debug logging
- commit `node_modules/`, `dist/`, `.next/`, or other build artifacts
- amend or force-push a commit someone else has based work on
