# 04 — Quality Gates and Definition of Done

**Applies to:** every project. A gate that is skipped is a gate that failed.

## 1. Canonical scripts

Every project exposes the same script names, regardless of stack:

```json
{
  "scripts": {
    "dev": "…",
    "build": "…",
    "lint": "eslint .",
    "typecheck": "tsc --noEmit",
    "test": "vitest run",
    "format:check": "prettier --check .",
    "check": "pnpm format:check && pnpm lint && pnpm typecheck && pnpm test && pnpm build"
  }
}
```

- Use `tsc -b` when the project uses TypeScript project references.
- Projects with no tests must state that in `AGENTS.md`; `check` then omits `test`. Do not add a fake test to satisfy the gate.
- The canonical gate is `pnpm check`. For npm projects, replace `pnpm` with `npm run` inside the `check` script.
- Prettier is the formatter; ESLint covers correctness. Do not add stylistic ESLint rules that duplicate Prettier.

Per stack:

| Stack | Typecheck | Test | Build |
|---|---|---|---|
| Next.js | `tsc --noEmit` | `vitest run` | `next build` |
| Astro | `astro check` | `vitest run` | `astro build` |
| Vite + React | `tsc -b` or `tsc --noEmit` | `vitest run` | `vite build` |

## 2. Required before every commit

- `format:check`, `lint`, `typecheck`, `test`, `build`
- no console errors in the development server
- security: no secrets in the diff, every env var documented, no high or critical advisories (rule 05)

For documentation-only changes, `build` may be skipped with a stated reason. Everything else still applies.

## 3. Continuous integration

- GitHub Actions runs on every PR and on `main`.
- Install with a frozen lockfile; cache the package manager store.
- CI runs the full `check` script.
- A Vercel build is not a substitute for CI checks.
- `main` stays green. Fix a red `main` before starting new work.
- Workflow: call the shared `web-ci.yml` from `dabaz-official/.github`, following [`templates/ci.yml`](../templates/ci.yml). The workflow installs and runs `pnpm check`; it does not restate the gate, so extending a project's gate never means editing the workflow.

## 4. Visual and UX gate

- Follow rule 08 for required widths, breakpoints, zoom, and keyboard checks.
- Check light and dark mode when the project supports both.
- Verify loading, empty, error, and disabled states.
- No layout shift, clipped text, or overlapping elements.
- Surface identity follows rule 10 when title, icons, OG, or manifest changed.
- UI changes include screenshots or a preview link in the PR.

## 5. Accessibility gate

Target WCAG 2.2 AA.

- No serious or critical axe violations.
- Every input has a label; every image has appropriate `alt`.
- Every icon-only button has an accessible name.
- Contrast follows `DabDesign/GUIDELINE.md` and the measured pairs in `core.md` or the project theme.
- Headings are semantic and ordered; landmarks are present.
- `prefers-reduced-motion` is respected.
- No keyboard trap; dialogs restore focus on close.

## 6. Performance gate

For public pages, run Lighthouse mobile and record the result:

| Metric | Threshold |
|---|---|
| Performance | ≥ 90 |
| Accessibility | ≥ 95 |
| Best Practices | ≥ 95 |
| SEO | ≥ 95 |
| LCP | ≤ 2.5 s |
| CLS | ≤ 0.1 |
| INP | ≤ 200 ms |
| Initial JS per route | ≤ 200 KB gzipped |

Project-specific exceptions go in `AGENTS.md` with a reason and review date. Do not quietly lower a threshold.

## 7. Testing strategy

- Test behavior and failure modes, not implementation details.
- Unit: pure logic, data transforms, validation, and edge cases, with Vitest.
- Component: user-visible behavior with React Testing Library; avoid snapshot-only tests.
- E2E: critical flows only (auth, checkout, publish, save), with Playwright.
- Every bug fix gets a regression test when practical.
- Coverage is not a target. Do not test third-party libraries or trivial markup.

## 8. Definition of Done

- [ ] Acceptance criteria met
- [ ] `pnpm check` passes
- [ ] Responsive checks (rule 08) and state checks (§4) pass
- [ ] Surface identity checked when changed (rule 10)
- [ ] Accessibility gate passes
- [ ] Performance gate passes or has a recorded exception
- [ ] Tests cover new behavior and regressions, or the no-test exception is recorded
- [ ] No console or server errors
- [ ] Docs updated if behavior, commands, or architecture changed
- [ ] Preview deploy checked for UI changes
- [ ] No secrets, debug logs, or commented-out code

## 9. Exceptions

- Record exceptions in `AGENTS.md`: rule, reason, owner, review date.
- Never skip a gate silently.
- If a rule is waived repeatedly across projects, amend the rule instead of accumulating exceptions.
