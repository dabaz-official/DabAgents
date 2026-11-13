# 06 — Deployment and Operations (Vercel)

**Applies to:** all web projects. Production is deployed from `main`, never from a laptop.

## 1. Environments

| Environment | Source | Purpose |
|---|---|---|
| Production | `main` | Public site |
| Preview | every branch / PR | Review, QA, client approval |
| Development | local | Day-to-day work |

Preview is the staging environment. Add a separate staging project only when preview isolation is insufficient, and record why in an ADR.

## 2. Vercel project setup

- One Vercel project per repository.
- Framework preset: Next.js, Astro, or Vite as appropriate; avoid manual overrides.
- Build command follows the stack: `next build`, `astro build`, `vite build` (output `dist`).
- Install with the committed lockfile; do not use `npm install` when the project uses pnpm.
- Pin the Node version in Vercel project settings and in `.nvmrc`.
- Root directory is the repository root. Use a monorepo only when there is a concrete need.

## 3. Environment variables

- Set variables in Vercel with the correct scope: Production, Preview, Development.
- Local development: `vercel env pull .env.local`.
- Changing a variable requires a redeploy; mention it in the PR.
- Values, validation, and preview isolation: rule 05 §1–§2.

## 4. Domains and DNS

- Production domain points at Vercel; choose one canonical host and redirect the other (apex ↔ `www`).
- HTTPS is automatic; enable HSTS after the domain is verified.
- DNS, domain, and certificate changes are user-approved actions. Do not change them unasked.
- Record the canonical URL in `AGENTS.md`.

## 5. Deploy and rollback

1. Merge to `main` after the gates pass (rules 03–04).
2. Vercel builds and deploys production.
3. Verify the deployment with the checklist below.
4. Tag the release if the project is versioned (rule 03).

- Never run `vercel --prod` from a local machine unless the user explicitly asks.
- Never edit build output or patch production manually.
- Roll back with Vercel's instant rollback to a known-good deployment.
- Database migrations must be backward compatible for at least one release so a rollback remains safe.

## 6. Caching

- Hashed static assets: `Cache-Control: public, max-age=31536000, immutable`.
- HTML: short-lived cache or revalidation; do not cache authenticated responses.
- Do not cache responses that vary by cookie, user, or authorization.
- Security headers: rule 05 §3. Configure redirects and rewrites in the framework config, not ad hoc in components.

## 7. Observability

- Enable Vercel Analytics and Speed Insights for public sites.
- Add error tracking (Sentry or equivalent) for server and client errors on production apps.
- Logs are structured and contain no secrets or personal data.
- Add an uptime check for critical routes when the project has users.
- Alerts go to a channel that is actually monitored.

## 8. Post-deploy checklist

- [ ] Production URL loads over HTTPS
- [ ] Key routes return 200; unknown routes return a real 404
- [ ] No console or server errors
- [ ] Environment-dependent features work (auth, forms, payments)
- [ ] Metadata and OG image are correct (rule 10)
- [ ] Lighthouse gate passes or has a recorded exception (rule 04 §6)
- [ ] Rollback target is known

## 9. Local production check

For major changes, run the production build locally before merging:

```sh
pnpm build && pnpm start   # Next.js
pnpm build && pnpm preview # Vite
pnpm build && pnpm preview # Astro
```

Do not ship a change that only works in the development server.
