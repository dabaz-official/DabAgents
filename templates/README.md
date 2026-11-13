# <Project name>

<One sentence describing what this is and who it is for.>

## Stack

- **Framework:** <Next.js App Router / Astro / Vite + React / Expo>
- **Language:** TypeScript, `strict: true`
- **Styling:** Tailwind CSS v4 + DabDesign tokens
- **Fonts:** DabFonts
- **Deploy:** Vercel

## Quick start

```sh
pnpm install
cp .env.example .env.local   # if the project has env vars
pnpm dev
```

Replace `pnpm` with the project's package manager if it is not pnpm.

## Scripts

| Command | Does |
|---|---|
| `pnpm dev` | Start the development server |
| `pnpm build` | Production build |
| `pnpm lint` | ESLint |
| `pnpm typecheck` | TypeScript check |
| `pnpm test` | Unit tests |
| `pnpm check` | Full gate: format, lint, typecheck, test, build |

## Environment

Required variables are listed in `.env.example`. Copy it to `.env.local` and fill in the values. Never commit `.env.local`.

## Deployment

Production deploys from `main` through Vercel. Every branch gets a preview URL. Rollback uses Vercel's instant rollback.

## Structure (optional)

```
app/ or src/     ...
```

## Documentation

- [`AGENTS.md`](AGENTS.md) — project contract, pinned guideline versions, commands, exceptions
- Design: DabDesign `GUIDELINE.md`
- Fonts: DabFonts `GUIDELINE.md`
