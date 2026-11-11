# 01 — Agent Operating Rules

**Applies to:** every task, every project. Read this before touching code.

## 1. Before you start

- Read the project's `AGENTS.md`, `README.md`, `package.json`, and the files you will change.
- For any UI work, start at `DabDesign/GUIDELINE.md` and follow the read order it defines (`core.md`, `GOVERNANCE.md`).
- For typography, punctuation, or font loading, start at `DabFonts/GUIDELINE.md` and follow the read order it defines (`TYPESETTING.md`).
- Inspect the repository state before assuming anything. Never invent file contents, APIs, or scripts.
- Restate the task in one sentence and outline the plan (3–6 steps). For non-trivial work, keep a todo list.
- If the repository contradicts the request, stop and ask instead of guessing.

## 2. Decide vs. ask

Ask before:

- destructive or irreversible actions: deleting data, force-pushing, rewriting history, schema migrations
- spending money, creating accounts, changing DNS or domains, publishing content
- adding a framework, a major dependency, or a new external service
- changing product behavior, copy, scope, or acceptance criteria
- handling credentials, tokens, or personal data

Decide yourself when the choice is:

- reversible
- conventional for the stack
- within the stated scope
- between equivalent implementations

When you decide, state the assumption in the final report.

## 3. Scope discipline

- Do only what the task asks. No drive-by refactors, renames, formatting, or "while I'm here" fixes.
- Keep diffs small and reviewable. If a change grows past the task, split it or ask.
- Do not add a dependency when the platform or an existing package already solves it.
- Do not modify unrelated files. If an unrelated fix is required, report it instead of doing it.
- Do not overwrite or revert the user's uncommitted work.

## 4. Verification

- Run the project's gates before claiming completion (rule 04).
- Report the exact commands run and their outcome. If a check fails or was skipped, say so with the output.
- Never claim "done", "fixed", or "passing" when typecheck, tests, or build have not run.
- For UI work, verify the rendered result at every width in `DabDesign/GUIDELINE.md` and check the console.
- If the same error persists after two focused attempts, stop and explain what you tried.

## 5. Design fidelity

- Follow `DabDesign/GUIDELINE.md`: semantic token roles only, no primitive ramps, no raw values, no local scales or component forks.
- Follow `DabFonts/GUIDELINE.md` for font files, weights, loading, punctuation, and mixed-script spacing. Do not download fonts ad hoc.
- Preserve contrast, focus visibility, and motion rules from the design system.
- Match existing patterns in the project before inventing a new one.

## 6. Git and remote

- Follow rule 03.
- Commit only changes made for the task.
- Never commit secrets, `.env` files, credentials, or generated build output.
- Do not push, force-push, rebase shared branches, open PRs, or publish releases unless asked.
- Never rewrite published history.

## 7. Communication

- Reply in the user's language. Write repository artifacts in English: docs, code, comments, commit messages, PR descriptions.
- Be concise. Report what changed, what was verified, and what remains.
- Surface risks, tradeoffs, and failures. Do not hide them behind optimistic summaries.
- No filler, no praise, no restating the request.

## 8. Definition of done

A task is done only when:

- acceptance criteria are met
- the gates in rule 04 pass
- docs are updated when behavior, commands, or architecture changed
- no secrets, debug logs, or commented-out code remain
- UI changes include a checked preview or screenshots

## 9. Stop conditions

Stop and ask when:

- requirements conflict or are ambiguous
- credentials, access, or a product decision are missing
- a gate fails for reasons unrelated to the task
- the requested change would break a published contract
- you are repeating the same failed approach
