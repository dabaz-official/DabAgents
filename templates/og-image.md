# Open Graph Image Layout

How to draw the 1200×630 image described in [rule 10](../rules/10-surface-identity.md) §5. Rule 10 owns the metadata fields; this file fixes the layout.

## Canvas

- Light theme only: `color-background` background, `color-text-primary` title, `color-text-secondary` supporting line.
- 80 px padding. Keep every element inside it.
- No gradients, screenshots, device frames, QR codes, or CTA buttons. A real product screenshot is allowed only when it is the page's subject and stays inside the padding.

## Elements

| Element | Type | Content |
|---|---|---|
| Wordmark | 24/600, top-left | Site name, official casing |
| Title | 48/600, max 2 lines | Page title |
| Supporting line | 24/400, max 1 line | Site tagline, ≤ 60 characters, identical on every image |
| Footer | 16/400, bottom | Canonical host left, year right |

- Do not repeat the site name in the title; the wordmark carries it.
- If the title does not fit two lines, shorten the page title. Never shrink the type or leave the padded area.
- All text is at least 4.5:1 against the background.
