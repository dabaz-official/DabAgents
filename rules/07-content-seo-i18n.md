# 07 — Content, SEO, and Internationalization

**Applies to:** all user-facing pages. `DabDesign/GUIDELINE.md` and `DabFonts/GUIDELINE.md` take precedence for tone and typesetting.

## 1. Language policy

- Every project declares its primary locale in `AGENTS.md`.
- One language per page. Bilingual layouts are allowed only when designed as such.
- Set the correct `lang` attribute on `<html>`.
- Do not ship unreviewed machine translation as production copy.
- Repository artifacts (docs, code, comments, commit messages) are in English; user-facing copy follows the project locale.
- Never build a sentence by concatenating translated fragments. Use full sentences with placeholders.
- Follow `DabFonts/GUIDELINE.md` for CJK punctuation spacing, CJK/Latin mixed-script spacing, and permitted weights.

## 2. Voice and microcopy

- Follow `DabDesign/GUIDELINE.md` and, for the personal series, `DabDesign.md` for voice: plain, direct, calm, editorial.
- Sentence case for headings, labels, and buttons. No exclamation marks. No marketing filler.
- Buttons name the action: "Save changes", not "Submit" or "OK".
- Errors state what happened and what to do next. No blame, no bare error codes.
- Empty states explain why the page is empty and offer the primary action.
- Destructive actions are confirmed and labeled with the consequence: "Delete project", not "Yes".
- Loading states are specific when the wait is long: "Loading projects…", not "Loading…".
- Use the same term for the same concept everywhere. Add it to a glossary if the project grows.

## 3. SEO

- Unique `<title>` per page, ≤ 60 characters, pattern `Page — Site`.
- Meta description, 120–160 characters, specific to the page.
- Canonical URL on every page.
- Open Graph and Twitter card metadata; OG image 1200×630.
- `sitemap.xml` and `robots.txt`; exclude drafts and private routes.
- One `<h1>` per page; headings follow a logical order.
- Structured data (JSON-LD) for articles, products, FAQs, and organization where relevant.
- Descriptive internal link text; never "click here".
- Real 404 responses; redirects for moved URLs; no soft 404s.
- Static content is preferred over client-rendered content for indexable pages.

## 4. Internationalization

- Use the framework's i18n support (for example `next-intl` or Astro i18n) when there is more than one locale.
- Put the locale in the URL (`/en/...`, `/zh/...`) or use another explicit, documented strategy.
- Format dates, numbers, currency, and relative time with `Intl`; never hand-format.
- Keep translated strings in locale files, not inline in components.
- Allow ~30% text expansion; do not bake text into images.
- Provide `hreflang` pairs and an `x-default`.
- Right-to-left support is required only when a project adds an RTL locale; plan layout with logical properties then.

## 5. Images and media

- Meaningful images have descriptive `alt`; decorative images use `alt=""`.
- Always set `width` and `height` (or `aspect-ratio`) to prevent layout shift.
- Serve responsive sizes and modern formats (AVIF/WebP).
- Compress before committing; do not commit multi-megabyte originals to `public/`.
- Video has captions; audio has a transcript.
- Critical information is never only inside an image.

## 6. Content structure

- Long-form content lives in content collections or MDX, not hardcoded in components.
- Frontmatter includes `title`, `description`, `date`, `draft`, and `locale` where relevant.
- Drafts are excluded from builds, sitemaps, and search.
- Articles show author and publication date.
- Keep copy in a single source per page; do not duplicate strings across templates.
