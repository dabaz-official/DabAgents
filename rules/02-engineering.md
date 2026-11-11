# 02 — Engineering Standards

**Applies to:** all web projects. Design values live in `DabDesign/GUIDELINE.md`; this document covers code.

## 1. Stack selection

Choose by project type. Do not mix stacks within one project.

| Project type | Default stack | Notes |
|---|---|---|
| Marketing site, web app | Next.js (App Router) + TypeScript + Tailwind CSS | Server components by default |
| Content, docs, blog | Astro + TypeScript + Tailwind CSS | Zero JS by default; islands only when interactive |
| Small tool, game, single page | Vite + React + TypeScript | Client-only; no router or state library until needed |
| Mobile / native | Expo + React Native | Only when native capabilities are required |

A new framework, rendering model, or styling system requires an ADR and the user's approval. Existing projects keep their current stack until deliberately migrated.

UI work also requires `DabDesign/GUIDELINE.md`; typography and font loading require `DabFonts/GUIDELINE.md`.

## 2. Runtime and packages

- **Node:** current Active LTS (even-numbered). Pin it in `.nvmrc` and `engines`.
- **Package manager:** pnpm for new projects. Existing npm projects may stay on npm. Exactly one lockfile per repository; never commit two.
- **TypeScript:** `strict: true`. No implicit `any`.
- **Dependencies:**
  - prefer maintained, small, well-typed packages
  - check license compatibility before adding
  - do not add a package for code shorter than ~20 lines
  - do not keep two libraries that solve the same problem
  - commit the lockfile; CI installs with a frozen lockfile
- **Formatting:** Prettier formats; ESLint checks correctness. Do not duplicate formatting rules in ESLint.

## 3. Project structure

These are defaults for new projects. Existing projects follow their current layout.

**Next.js (App Router)**

```
app/                 routes, layouts, route groups, error/loading boundaries
components/          shared components; components/ui for primitives
lib/                 utilities, data access, config, validation
content/             MDX or data files
public/              static assets
```

- Server components by default; add `"use client"` at the leaf that needs state, effects, or browser APIs.
- Fetch data in server components or route handlers, not in client effects for first paint.
- Route handlers validate input and return typed responses.
- Do not create `src/` unless the project already uses it.

**Astro**

```
src/pages/           file-based routes
src/layouts/         page shells
src/components/      components; interactive islands marked as such
src/content/         content collections
src/styles/          tokens and global CSS
```

- Ship zero JS unless a component is interactive.
- Use content collections for long-form content, not hardcoded component arrays.

**Vite + React**

```
src/features/<feature>/   feature components, hooks, logic
src/components/           shared UI
src/lib/                  utilities and adapters
src/styles/               tokens and global CSS
```

- Feature-first. No premature router, global store, or data layer.

**General**

- Use the `@/` path alias for project-internal imports.
- One component per file. Avoid barrel files except for a deliberate public API.
- Colocate tests with code or in a nearby `__tests__/` directory.
- Never commit `node_modules/`, `dist/`, `.next/`, or other build output.

## 4. Naming

- Files and directories: `kebab-case`.
- React components: `PascalCase`.
- Hooks: `useSomething`.
- Types and interfaces: `PascalCase`, no `I` prefix.
- Constants: `UPPER_SNAKE_CASE`.
- Environment variables: `UPPER_SNAKE_CASE`.
- URLs and route segments: `kebab-case`.
- Booleans read as predicates: `isOpen`, `hasError`, `canPublish`.

## 5. TypeScript

- Model variants with discriminated unions, not piles of optional flags.
- Validate external data at the boundary with `zod`: API responses, form input, environment variables, URL params.
- Export types from the module that owns the data.
- Avoid `enum`; use union types or `as const` objects.
- No `@ts-ignore` or `as any` without a comment explaining why and a linked issue.
- Prefer `unknown` over `any` at boundaries and narrow explicitly.

## 6. Styling

- Follow `DabDesign/GUIDELINE.md` for token roles, typography, space, shape, layout, and icon rules.
- Tailwind CSS v4 with DabDesign tokens exposed as CSS variables.
- Use semantic roles (`color-text-primary`, `type-body`), never primitive ramps (`gray-900`, `blue-600`), and never raw hex, px, or ms values where a token exists.
- Use the project's `cn()` helper (`clsx` + `tailwind-merge`) for conditional classes.
- No arbitrary values (`w-[437px]`, `text-[#123456]`) unless no token exists; if repeated, propose a token through DabDesign's decision process.
- No inline styles except computed values (positions, transforms from measurements).
- No second styling system (CSS modules, styled-components, MUI) in a Tailwind project.
- Mobile-first. Use the breakpoints in `DabDesign/GUIDELINE.md`, not ad-hoc media queries.
- Dark mode comes from theme tokens, not per-component overrides.
- Global CSS is limited to tokens, resets, and base element styles.
- Respect `prefers-reduced-motion`; animation is functional, not decorative.

## 7. Components

- Props are typed and minimal. No prop drilling beyond two levels; use composition or context instead.
- Handle loading, empty, error, and disabled states explicitly.
- Accessibility is part of the component: labels, roles, focus management, keyboard behavior.
- Follow `DabDesign/GUIDELINE.md` §9 for component status. The v1 pilot set is Button, Text input, and Card; do not treat `components/` or previews as the current contract.
- Prefer server components; move interactivity into small client leaves.

## 8. Data, state, and APIs

- Local state first. Lift state only when shared.
- Put shareable filters and pagination in the URL.
- Keep server state on the server. Do not duplicate it into a global client store.
- Add a global store only after cross-tree state is proven necessary.
- API responses are typed and validated. Errors use a consistent shape:

```json
{ "error": { "code": "not_found", "message": "Project not found" } }
```

- Use correct status codes. Never return `200` with an error payload.
- Only `NEXT_PUBLIC_*` / `VITE_*` values reach the client. Treat them as public.

## 9. Error handling and logging

- User-facing errors state what happened and what to do next; no stack traces or internal codes alone.
- Server errors are logged with context. Never log secrets or personal data.
- Add route-level error boundaries (Next `error.tsx`, React error boundaries).
- Do not swallow errors with empty `catch` blocks.
- Unexpected states fail loudly in development and degrade gracefully in production.

## 10. Performance defaults

- Prefer static rendering or server rendering; hydrate only interactive parts.
- Lazy-load heavy client code and below-the-fold widgets.
- Optimize images (`next/image`, Astro assets), set dimensions, and serve modern formats.
- Follow `DabFonts/GUIDELINE.md` for font files, `@font-face`, weights, fallbacks, and typesetting. Self-host fonts, use `font-display: swap`, and preload only critical files.
- Check bundle impact before adding a client dependency.
- No blocking third-party scripts; load analytics after interaction or with `defer`.

## 11. Dependency hygiene

- Commit the lockfile and use frozen installs in CI.
- Remove unused dependencies when you touch the project.
- Run a security audit before releases (rule 05).
- Pin the Node and package-manager versions in `package.json` (`packageManager` field).
- Review new packages for maintenance status, download size, transitive dependencies, and license.
