# AGENTS.md — Project Contract

> Copy this file to the project root and fill it in. Keep it under one page.
> This file is the only document an agent must read before starting; it pins everything else.

## Project

- **Name:**
- **Purpose:** (one sentence)
- **Repo:**
- **Primary locale:** (e.g. `en`, `zh-CN`; mixed pages are not allowed unless intentional)
- **Owner:**

## Required reading (in order)

1. **DabAgent-Guideline** @ `<tag or commit SHA>` — `<url>`
2. **DabDesign** @ `<tag or commit SHA>` — design tokens, components, contrast, voice
3. **DabFonts** @ `<tag or commit SHA>` — font files and loading (omit if the project uses DabDesign's vendored fonts)

## Stack

- **Framework:** (Next.js App Router / Astro / Vite + React / Expo)
- **Language:** TypeScript, `strict: true`
- **Styling:** Tailwind CSS v4 + DabDesign tokens
- **Package manager:** pnpm (existing projects: state the actual one)
- **Node:** current Active LTS, pinned in `.nvmrc`
- **Deploy:** Vercel

## Commands

```sh
pnpm dev
pnpm build
pnpm lint
pnpm typecheck
pnpm test
pnpm format:check
pnpm check        # full gate: format + lint + typecheck + test + build
```

## Definition of Done

- [ ] Acceptance criteria met
- [ ] `pnpm check` passes
- [ ] Responsive at 375 / 768 / 1440
- [ ] Keyboard + focus + contrast checked
- [ ] No console or server errors
- [ ] Loading, empty, and error states handled
- [ ] Docs updated (`README`, `AGENTS.md`, ADR, changelog) if behavior changed
- [ ] No secrets, debug logs, or commented-out code

## Project-specific rules

- (e.g. content collections live in `src/content`; API routes require auth; no client-side data fetching for first paint)

## Exceptions

Record any waived rule here with a reason and a review date. Never skip a gate silently.

- (e.g. Lighthouse Performance 85 instead of 90 — heavy map on `/explore`; revisit 2027-01-31)
