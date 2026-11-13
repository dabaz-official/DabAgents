# 10 — Surface Identity

**Applies to:** every user-facing site. Rule 07 owns content, SEO, and locale ranges; this document owns the surfaces a user or crawler sees before the page: title, description reuse, icons, Open Graph, manifest, and browser colors.

## 1. One source of truth

- Put the site name, tagline, canonical origin, primary locale, default description, theme colors, icon paths, and OG size in one `siteConfig` module.
- The site name has one casing everywhere: `<title>`, `og:site_name`, manifest, wordmark, and footer.
- A page owns only its page title and description. It never repeats the site name.
- The page title, `<h1>`, `og:title`, and `twitter:title` are the same string. The full `<title>` carries the site name once: at the end everywhere, at the start on the home route.

| Field | Value |
|---|---|
| `<title>` | `<page title> — <site name>` |
| `<title>` on the home route | `<site name> — <tagline>` |
| `<h1>` | `<page title>` |
| `meta[name="description"]` | page description |
| `og:title`, `twitter:title` | `<page title>` |
| `og:site_name` | `<site name>` |
| `og:description`, `twitter:description` | page description |
| `og:image`, `twitter:image` | route image or site default |
| `og:image:alt`, `twitter:image:alt` | `<page title>` |
| `og:url`, `link[rel="canonical"]` | absolute page URL |
| `og:locale` | locale with underscore: `en_US`, `zh_CN` |
| `og:type` | `website`, or `article` for articles |
| `twitter:card` | `summary_large_image` |

## 2. Page title

Pattern: `<page title> — <site name>`. Home route: `<site name> — <tagline>`.

- Separator: em dash `—` (U+2014) with one space on each side. No `|`, `-`, `:`, `·`, or `•` between page and site.
- Order: page first, site last, except on the home route, where the site name leads and the tagline follows.
- Home route: `/` or one locale segment (`/en`, `/zh`), with or without a trailing slash, including the default locale served unprefixed. Nothing deeper. Its page title stays the tagline, so `<h1>`, `og:title`, and `twitter:title` remain the tagline; only `<title>` puts the site name first. Localized pages such as `/en/pricing` use the page-first pattern.
- Page part: sentence case, no trailing period, no "Home", "Welcome", or "Page". Keep acronyms and product names as written.
- Site name: official casing, once, at the start on the home route and at the end everywhere else.
- The `<h1>` is the page title without the site name. One `<h1>`.
- Length budget: 60 character units for the whole `<title>`, counting each CJK character as 2. Shorten the page title or the tagline, never the site name.
- Utility pages follow the same pattern: `404 — Site`, `Sign in — Site`.

## 3. Description

- One description string per page. The same string is used for `meta[name="description"]`, `og:description`, and `twitter:description`.
- Length follows rule 07's language table. Count code points. Do not pad.
- The home page uses the site's default description; every other page writes its own.
- The OG image's supporting line is the site tagline, not the meta description.

## 4. Icons

Masters: one or two square SVGs, 512×512 viewBox, flat mark, no words or taglines, no gradients. The mark stays inside the central 80% safe area.

| Master | Background | Used for |
|---|---|---|
| Plate | Full background or plate with baked corners | `apple-icon.png`, `icon-maskable-512.png` |
| Mark | Transparent | `favicon.ico`, `icon.svg`, `icon-192.png`, `icon-512.png` |

- If one SVG is supplied, it is the plate master and covers every surface. If two are supplied, the plate master covers iOS and maskable, and the mark master covers browser and standard manifest icons.
- If the only supplied SVG is a transparent mark, use it for browser and standard manifest icons, and ask before generating iOS or maskable surfaces.
- Treat each master as the source of truth for its surfaces: do not re-round, pad, crop, or fill the plate's transparent corners; do not add a background to the mark master. Preserve supplied alpha.
- The plate master uses the light-theme `color-primary` background and `color-on-primary` mark. It does not switch with the color scheme.
- The mark master keeps its supplied colors and transparent background; do not recolor it unless the owner asks.
- Baked corners are allowed on the plate. Keep the radius at or below the platform mask: iOS uses a squircle of about 22.4% of the side, and a larger radius is clipped by the mask instead of honored.
- A supplied plate needs no extra background when its radius is at or below the platform mask and it covers the central 80% circle. Do not add a second plate.
- Plate exports may keep transparent corners; they are the only transparent area, with no holes inside the plate. On the maskable export the plate still covers the central circle of 80% diameter, so a circular launcher crop never shows the background through it.
- Test the mark at 16×16. If it is unreadable, simplify the mark; do not add a second favicon.

| File | Size / format | Purpose |
|---|---|---|
| `app/favicon.ico` | 16, 32, 48 multi-resolution ICO | Browser tab, legacy |
| `app/icon.svg` | scalable, 1:1 | Modern browser tab |
| `app/apple-icon.png` | 180×180 PNG | iOS home screen |
| `public/icons/icon-192.png` | 192×192 PNG | Manifest |
| `public/icons/icon-512.png` | 512×512 PNG | Manifest, splash |
| `public/icons/icon-maskable-512.png` | 512×512 PNG, 80% safe zone | Maskable |

- One Apple icon size: 180×180. Do not ship a size matrix.
- Non-Next stacks use the same sizes under `public/` and link them in `<head>` and the manifest.
- Manifest: `name` = site name, `short_name` ≤ 12 characters, `start_url` = `/`, `display` = `standalone`, `lang` = primary locale, `dir` = `ltr` or `rtl`. `background_color` and `theme_color` use the light `color-background`.
- `theme-color` has two entries, light and dark, both `color-background`. Set `color-scheme: light dark`.
- `apple-mobile-web-app-title` is the site name; the status bar is `default`. Do not add a splash-screen matrix.
- No `msapplication-*` tile meta and no Safari pinned-tab `mask-icon` unless the brand has an approved monochrome mark; the manifest and SVG favicon cover those surfaces.

## 5. Open Graph and Twitter

- One image size: 1200×630 px, 1.91:1. No other sizes. One template for generated images; pages vary only the page title.
- Light theme only. Layout and type: [`templates/og-image.md`](../templates/og-image.md).
- The home OG image is a custom asset supplied by the owner. Use it when present. Generate a home image only when none is supplied.
- Generated page image: title = page title, supporting line = site tagline (≤ 60 characters).
- Generated home image: title = site name, supporting line = site tagline. Do not use the tagline as the title; it would repeat.
- File: PNG, sRGB, ≤ 5 MB hard limit, target ≤ 300 KB. One default image per site; routes may override it. Pages without custom art use the default.
- `og:image:alt` = page title, ≤ 125 characters.
- Twitter uses the same image and copy with `summary_large_image`. If the framework needs a separate file, re-export the same generator; do not design a second image.
- Add `twitter:site` or `twitter:creator` only when the project has an official account; never invent a handle.

## 6. Checks

- [ ] `<title>` matches `<page> — <site>` on every route except the home route, which matches `<site> — <tagline>`; one em dash, sentence case, one site name, within budget.
- [ ] `<h1>`, `og:title`, and `twitter:title` equal the page title; `<h1>` appears once.
- [ ] Meta, OG, and Twitter descriptions are the same string and within the rule 07 range.
- [ ] `favicon.ico` has 16/32/48; `icon.svg` and the 180×180 Apple icon exist.
- [ ] On the plate export, the baked corner radius stays within the platform mask and transparency appears only outside the plate; the mark is readable at 16×16.
- [ ] Each supplied master is 512×512 with the mark inside the 80% safe area; the plate's radius is within the platform mask and covers the 80% circle.
- [ ] Derivatives preserve the assigned master's alpha: no re-rounding, padding, filling the plate's transparent corners, or adding a background to the mark.
- [ ] Manifest lists 192 and 512 from the mark master and maskable 512 from the plate; the maskable plate matches the light background; `theme-color` has light and dark entries.
- [ ] OG image is 1200×630, light theme, 80 px padding, and reused for Twitter; home uses the supplied custom image, and the generated fallback titles the site name above the tagline.
- [ ] A metadata test asserts the title pattern, description range, canonical URL, OG size, and icon files.
