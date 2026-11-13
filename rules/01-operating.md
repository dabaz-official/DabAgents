# 01 — Operating Rules

**Applies to:** every task in every web project. This is the only rule you read by default.

## 1. Task loop

1. Read the project's `AGENTS.md` and `README.md`; inspect `package.json` and the files you will change.
2. Classify the task with the routing table in §6. Load only the rules whose trigger fires.
3. Restate the task in one sentence and outline a 3–6 step plan.
4. Implement the smallest change that satisfies the task.
5. Run the project's gates (rule 04) and verify the result.
6. Report what changed, what was verified, and what remains.

Use the guideline version pinned by the project. If there is no pin, use `main` and say so in the report. If the project's `AGENTS.md` opts out, do not apply this guideline.

Do not load every rule. Do not start without a plan.

## 2. Ask vs. decide

Ask before:

- destructive or irreversible actions: deleting data, force-pushing, rewriting history, schema migrations
- spending money, creating accounts, changing DNS or domains, publishing content
- adding a framework, a major dependency, or a new external service
- changing product behavior, copy, scope, or acceptance criteria
- handling credentials, tokens, or personal data

Decide yourself when the choice is reversible, conventional for the stack, within scope, and between equivalent implementations. State the assumption in the report.

## 3. Scope discipline

- Do only what the task asks. No drive-by refactors, renames, formatting, or "while I'm here" fixes.
- Keep diffs small and reviewable. If a change grows past the task, split it or ask.
- Do not add a dependency when the platform or an existing package already solves it.
- Do not modify unrelated files. Report an unrelated fix instead of doing it.
- Do not overwrite or revert the user's uncommitted work.

## 4. Verification and reporting

- Run the gates before claiming completion (rule 04).
- Report the exact commands run and their outcome. If a check fails or was skipped, say so with the output.
- Never claim "done", "fixed", or "passing" when typecheck, tests, or build have not run.
- For UI work, verify every width in `DabDesign/GUIDELINE.md` and check the console.
- If the same error persists after two focused attempts, stop and explain what you tried.
- Reply in the user's language. Write repository artifacts in English.
- Surface risks and failures. No filler, no praise, no restating the request.

## 5. Stop conditions

Stop and ask when:

- requirements conflict or are ambiguous
- credentials, access, or a product decision are missing
- a gate fails for reasons unrelated to the task
- the requested change would break a published contract
- you are repeating the same failed approach

## 6. Routing table

Load a rule only when its trigger fires.

| When the task touches | Read |
|---|---|
| code: stack, structure, TypeScript, styling, components, data, dependencies, performance | [02](02-engineering.md) |
| branches, commits, PRs, reviews, releases, hotfixes | [03](03-workflow.md) |
| gates, CI, Definition of Done, testing, accessibility, performance budgets | [04](04-quality.md) |
| secrets, environment variables, auth, headers, privacy | [05](05-security.md) |
| Vercel, domains, deploys, rollback, observability | [06](06-deployment.md) |
| copy, SEO, i18n, media, content structure | [07](07-content.md) |
| browsers, responsive layout, input, CSS/JS support | [08](08-compatibility.md) |
| README, AGENTS.md, ADRs, changelog, comments | [09](09-docs.md) |
| title, icons, Open Graph, manifest, theme colors | [10](10-surface-identity.md) |

Dependency entry points:

- UI work: start at `DabDesign/GUIDELINE.md`, then follow its read order (`core.md`, `GOVERNANCE.md`).
- Typography, punctuation, font loading: start at `DabFonts/GUIDELINE.md`, then `TYPESETTING.md`.

Whatever rule you load, never hardcode design values, commit secrets, or push without being asked.

## 7. Done

"Done" means the Definition of Done in [rule 04 §8](04-quality.md) is complete. Do not invent a weaker definition.
