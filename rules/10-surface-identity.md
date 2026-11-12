# 10 — Surface Identity

**Applies to:** every user-facing site. Rule 07 owns content, SEO, and locale ranges; this document owns the surfaces a user or crawler sees before the page: title, description reuse, icons, Open Graph, manifest, and browser colors.

## 1. One source of truth

- Put the site name, tagline, canonical origin, primary locale, default description, theme colors, icon paths, and OG size in one `siteConfig` module.
- The site name has one casing everywhere: `<title>`, `og:site_name`, manifest, wordmark, and footer.
- A page owns only its page title and description. It never repeats the site name.
- The page title, `<h1>`, `og:title`, and `twitter:title` are the same string. The full `<title>` appends the site name once.

| Field | Value |
|---|---|
| `<title>` | `<page title> — <site name>` |
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

Pattern: `<page title> — <site name>`

- Separator: em dash `—` (U+2014) with one space on each side. No `|`, `-`, `:`, `·`, or `•` between page and site.
- Order: page first, site last. Home uses the site tagline as the page title: `<tagline> — <site>`.
- Page part: sentence case, no trailing period, no "Home", "Welcome", or "Page". Keep acronyms and product names as written.
- Site name: official casing, once, at the end.
- The `<h1>` is the page title without the site name. One `<h1>`.
- `og:title` and `twitter:title` are the page title, not the full `<title>`; `og:site_name` carries the site.
- Length budget: 60 character units, counting each CJK character as 2. Shorten the page title, never the site name.
- Utility pages follow the same pattern: `404 — Site`, `Sign in — Site`.

## 3. Description

- One description string per page. The same string is used for `meta[name="description"]`, `og:description`, and `twitter:description`.
- Length follows rule 07's language table. Count code points. Do not pad.
- The home page uses the site's default description; every other page writes its own.
- The OG image's supporting line is the site tagline, not the meta description.

## 4. Icons

Master: one square SVG, 512×512 viewBox, flat mark, no words or taglines, no gradients. The mark stays inside the central 80% safe area; the background fills the canvas.

- Icon files use the light-theme `color-primary` background and `color-on-primary` mark. They do not switch with the color scheme.
- No rounded corners baked in; the OS applies its mask.
- No transparency in the Apple or maskable PNGs.
- Test the mark at 16×16. If it is unreadable, simplify the mark; do not add a second favicon.

| File | Size / format | Purpose |
|---|---|---|
| `app/favicon.ico` | 16, 32, 48 multi-resolution ICO | Browser tab, legacy |
| `app/icon.svg` | scalable, 1:1 | Modern browser tab |
| `app/apple-icon.png` | 180×180 PNG, opaque | iOS home screen |
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

- One image size: 1200×630 px, 1.91:1. No other sizes. One template for the whole site; pages vary only the page title.
- Light theme only. Layout and type: [`templates/og-image.md`](../templates/og-image.md).
- Title = page title. Supporting line = site tagline (≤ 60 characters), the same on every image.
- File: PNG, sRGB, ≤ 5 MB hard limit, target ≤ 300 KB. One default image per site; routes may override it. Pages without custom art use the default.
- `og:image:alt` = page title, ≤ 125 characters.
- Twitter uses the same image and copy with `summary_large_image`. If the framework needs a separate file, re-export the same generator; do not design a second image.
- `og:description` is the meta description. Do not write a second description.
- `og:type` is `website` except article pages, which use `article`.
- Add `twitter:site` or `twitter:creator` only when the project has an official account; never invent a handle.

## 6. Checks

- [ ] `<title>` matches `<page> — <site>`; one em dash, sentence case, one site name, within budget.
- [ ] `<h1>`, `og:title`, and `twitter:title` equal the page title; `<h1>` appears once.
- [ ] Meta, OG, and Twitter descriptions are the same string and within the rule 07 range.
- [ ] `favicon.ico` has 16/32/48; `icon.svg` and the 180×180 opaque Apple icon exist.
- [ ] Manifest lists 192, 512, and maskable 512; colors match the light background.
- [ ] `theme-color` has light and dark entries.
- [ ] OG image is 1200×630, light theme, 80 px padding, and the same image is used for Twitter.
- [ ] A metadata test asserts the title pattern, description range, canonical URL, OG size, and icon files.
