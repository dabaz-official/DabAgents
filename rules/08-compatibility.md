# 08 — Compatibility and Responsive Policy

**Applies to:** all web projects. Target modern evergreen browsers; do not carry legacy support by default.

## 1. Browser support

- Last two stable versions of Chrome, Edge, Firefox, and Safari (desktop and iOS).
- Android Chrome: last two stable versions.
- No Internet Explorer, no legacy Edge, no Opera Mini.
- Prefer Baseline "widely available" features. Check MDN or caniuse before using a newer API.
- If a feature is not broadly available, provide a fallback or ask; do not silently break older browsers.
- Record any project-specific support change in `AGENTS.md`.

## 2. Responsive rules

- Mobile-first. Minimum supported width: 360 px.
- Use the breakpoints defined in DabDesign; no ad-hoc media queries.
- Test at 375, 768, 1024, and 1440 px.
- No horizontal scrolling at 320 px or at 200% zoom.
- Touch targets are at least 44×44 px with adequate spacing.
- Hover is an enhancement only. Every hover-revealed action must also work on touch and keyboard.
- Respect safe-area insets on iOS (`env(safe-area-inset-*)`) for fixed bars and full-height layouts.

## 3. Input and devices

- All interactive UI is keyboard-operable with a visible focus state.
- Forms use correct `type`, `inputmode`, `autocomplete`, and `enterkeyhint`.
- Enter submits a single-line form; Escape closes dialogs and menus.
- Labels are always visible or programmatically associated; placeholders are not labels.
- No hover-only menus, scroll-jacking, or custom scrollbars that hide content.
- Honor `prefers-reduced-motion` and `prefers-color-scheme`.
- Do not hardcode pure black or white; use theme tokens so dark mode works.

## 4. CSS and JavaScript

- Progressive enhancement: core content and navigation work without client JS where practical.
- Feature-detect with `@supports`, `in`, or capability checks; never sniff the user agent.
- Avoid browser-specific hacks unless documented with a comment and a removal condition.
- Do not block rendering on third-party scripts.
- Keep CSS layers predictable: tokens, base, components, utilities. No `!important` except for documented overrides.

## 5. Testing

- If the project has end-to-end tests, run them on Chromium and WebKit.
- Manually check the current Safari (desktop and iOS) and Chrome before a release.
- Check the smallest supported width, the largest layout, and a zoomed view.
- Report unsupported combinations honestly; do not silently drop a feature.
- Add a regression test when fixing a browser-specific defect.
