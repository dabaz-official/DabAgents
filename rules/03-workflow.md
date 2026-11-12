# 03 — Git and Delivery Workflow

**Applies to:** every repository. `main` is always deployable.

## 1. Branching

- Work trunk-based: short-lived branches from `main`, merged back quickly.
- Branch names: `feat/<slug>`, `fix/<slug>`, `chore/<slug>`, `docs/<slug>`, `refactor/<slug>`.
- Keep a branch alive for less than three days. Split large work instead.
- Solo exception: documentation, typo, and one-line fixes may go directly to `main`. Anything touching behavior uses a branch.

## 2. Commits

Use Conventional Commits:

```
type(scope): imperative summary

Why this change is needed, not what the diff shows.
```

- Types: `feat`, `fix`, `refactor`, `perf`, `docs`, `test`, `build`, `ci`, `chore`, `revert`.
- Summary: imperative, lowercase, no trailing period, ≤72 characters.
- One logical change per commit. Never mix formatting with behavior.
- Body explains the reason and any tradeoff. Reference issues when they exist.
- Do not commit secrets, `.env` files, build output, or unrelated files.

Examples:

```
feat(resume): add print stylesheet
fix(nav): restore focus after dialog close
chore(deps): upgrade next to 16.1.0
docs(agents): pin design system version
```

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

## 4. Review checklist

- [ ] Matches the acceptance criteria; no unrelated changes
- [ ] Gates pass (rule 04)
- [ ] UI changes include screenshots or a preview link
- [ ] Docs updated if behavior, commands, or architecture changed
- [ ] Risks and rollback notes are in the PR

## 5. Releases and versioning

- Use semantic versioning: `MAJOR.MINOR.PATCH`.
- Tag production releases: `vX.Y.Z`.
- Maintain `CHANGELOG.md` for released projects; user-visible changes only.
- Breaking changes require a major bump and a migration note.
- Deploy production from `main` only.
- Do not move or reuse a published tag.

## 6. Hotfixes

- Branch from `main`, make the smallest safe fix, open a PR, deploy, tag a patch release.
- Do not bundle unrelated changes into a hotfix.
- If the process failed, add a short root-cause note to the PR or an ADR.

## 7. Never do

- force-push `main` or a shared branch
- rewrite published history
- commit `.env`, keys, tokens, or credentials
- merge with failing gates
- commit commented-out code or debug logging
- commit `node_modules/`, `dist/`, `.next/`, or other build artifacts
- amend or force-push a commit someone else has based work on
