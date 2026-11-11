# 05 — Security and Privacy

**Applies to:** every project, including internal tools. Assume every client-visible value is public.

## 1. Secrets

- Never commit `.env`, `.env.local`, `.env.*.local`, keys, tokens, or credentials.
- Commit `.env.example` with variable names, purposes, and placeholder values only.
- Local secrets live in `.env.local`. CI and production secrets live in the Vercel dashboard.
- `NEXT_PUBLIC_*` and `VITE_*` are embedded in the client bundle. Never put a secret there.
- Never print secrets in logs, error messages, screenshots, issues, or analytics.
- If a secret leaks: rotate it first, then remove it from history. Assume it is compromised.
- Use least-privilege tokens and separate personal, CI, and production credentials.

## 2. Environment contract

- Every variable is listed in `.env.example` with a one-line purpose.
- Validate required variables at startup with `zod`; fail fast and clearly.
- Use separate values per Vercel environment (Development, Preview, Production).
- Preview deployments must never point at production databases or paid services.
- Changing a variable requires a redeploy; document that in the PR.

## 3. Web security baseline

- HTTPS only; redirect HTTP to HTTPS; enable HSTS after verification.
- Send these headers in production:

| Header | Value |
|---|---|
| `X-Content-Type-Options` | `nosniff` |
| `Referrer-Policy` | `strict-origin-when-cross-origin` |
| `Permissions-Policy` | disable unused features (`camera=(), microphone=(), geolocation=()`) |
| `X-Frame-Options` / `frame-ancestors` | deny framing unless embedding is intentional |
| `Strict-Transport-Security` | `max-age=63072000; includeSubDomains; preload` after verification |

- Add a Content Security Policy. Start in report-only mode, fix violations, then enforce. Avoid `unsafe-inline` and `unsafe-eval` where possible.
- Cookies: `HttpOnly`, `Secure`, `SameSite=Lax` (or `Strict` where safe). Never store session tokens in `localStorage`.
- Protect state-changing requests against CSRF: same-site cookies plus origin checks or tokens.
- Validate and sanitize all input at the server boundary. Encode output.
- If HTML must be rendered raw, sanitize it (for example with DOMPurify); never pass user input to `dangerouslySetInnerHTML`.
- Rate-limit authentication and public write endpoints.
- Allowlist redirect targets; never accept arbitrary return URLs.

## 4. Authentication and authorization

- Do not implement your own cryptography or session protocol.
- Use an established provider or library (Auth.js, Clerk, Supabase Auth, or equivalent); record the choice in an ADR.
- Sessions expire and refresh; provide a way to sign out all devices.
- Enforce authorization on the server and at the data layer, not only by hiding UI.
- Protect admin routes in middleware and again in the handler that reads or writes data.
- Never trust a user ID, role, or price sent by the client.

## 5. Dependencies and supply chain

- Commit the lockfile; install with a frozen lockfile in CI.
- Review new packages before adding: maintenance, downloads, transitive dependencies, license, install scripts.
- Do not run unknown `postinstall` scripts. Prefer packages that do not need them.
- Run an audit before releases; no high or critical advisories in production dependencies.
- Enable Dependabot or equivalent and review its PRs like any other change.
- Remove unused packages; every dependency is attack surface.

## 6. Privacy

- Collect the minimum data needed. Do not add tracking by default.
- No personal data in analytics, logs, URLs, or error reports.
- Use cookie consent when non-essential cookies or trackers are present.
- Publish a privacy page when the project collects personal data.
- Define retention; delete data when it is no longer needed.
- Review third-party scripts. No session replay or ad pixels without consent.

## 7. Reporting

- Suspected vulnerability: stop the task, do not deploy, tell the owner.
- Leaked credential: rotate immediately, then clean history and redeploy.
- Never hide or downgrade a security concern to finish a task faster.
