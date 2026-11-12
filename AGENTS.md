# AGENTS.md

This repository is a **guidelines repository**, not an application. It has no build, tests, or deploy target.

## When editing this repository

- Write documentation in English. Conversation with the user follows the user's language.
- Keep rules short, concrete, and checkable. Prefer a command or checklist over an aspiration.
- Do not duplicate design tokens, font files, or component specs from DabDesign or DabFonts; link to their `GUIDELINE.md` entry points instead.
- When adding a rule, state the failure it prevents in the PR description.
- Update the index in `README.md` when adding or renaming a document.
- Keep numbering stable. Do not renumber existing documents for a new topic; append with the next free number.
- Remove a rule that is repeatedly waived rather than adding exceptions around it.

## Structure

```
README.md                  index and source-of-truth contract
AGENTS.md                  this file — rules for editing the guidelines
rules/01..10               the guidelines themselves
templates/AGENTS.md        per-project contract template
```

## When working in another project

Do not follow this file there. Copy `templates/AGENTS.md` into that project and follow its pinned versions of these rules.
