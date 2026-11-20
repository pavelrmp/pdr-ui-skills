# Brand loader

Figma page: **Brand loader 🟢** `10826:963` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10826-963) · Figma Spec: [`11032:4612`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11032-4612)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Brand loader/Mark`, `Brand loader/Progress loader`, `Brand loader/Wordmark` (building blocks: `.Brand loader module 2 / 2-1 / 2-2`) · **Angular:** inline SVG with CSS animation (`pathLength="1"`); component selector to confirm · **Sources:** guidelines on this page and the component descriptions

> **No M3 component.** The brand loader is a PDR brand moment. All rules below come from the guidelines on this page.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

The animated PDR.cloud logo marks moments when the **whole product** is getting ready — signing in, loading the workspace, signing out. It’s a brand moment, **not** a general loading pattern.

| Use | Component |
|---|---|
| **Login** — after credentials / MFA are submitted, while session, profile and permissions load | `Brand loader/Wordmark` |
| **App start** — loading the key features on first entry or after switching company / location | `Brand loader/Progress loader` (or `Mark` at the end) |
| **Logout** — while the session ends and local data is cleared | `Brand loader/Wordmark` |
| Reduced-motion fallback and final frame | `Brand loader/Mark` |

**Don’t use**

- Lists, tables, cards, panels → **Skeleton**.
- Buttons, fields, inline saves → **Circular progress (24)**.
- Uploads or measurable tasks → **Linear progress (determinate)**.
- **Never** inside dialogs, and **never** more than one on screen.

## Anatomy

| Component | Content |
|---|---|
| Mark | Static logo from 11 segments |
| Progress loader | Animated mark: 2 s loop, segments draw on one after another (≈0.1 s stagger, ≈0.4 s each, cubic-bezier(0.5, 0, 0.5, 1)), then the full mark holds |
| Wordmark | Mark draws on (0–1.4 s), then slides left while the PDR.cloud wordmark is revealed (≈1.3–1.6 s, ease-out); nests Progress loader |
| Segments | `.Brand loader module` building blocks — internal only |

## Decision rules

1. **MUST** show it full-screen and centred on the surface background.
2. Login and Logout → `Wordmark`; App start → `Progress loader`.
3. **MUST** use these components — never redraw, detach or re-colour the logo. **MUST NOT** place the segment modules directly in designs.
4. **SHOULD** show it only when the wait is longer than ~400 ms; once shown, keep it for at least ~1 s so it doesn’t flash.
5. MAY show a status text below the logo: “Signing you in…”, “Loading your workspace…”, “Signing you out…”. For long waits (~10 s), update the text as described on this page.
6. With reduced motion, show `Brand loader/Mark` instead of the animation.

## Developer notes

- Export as inline SVG with un-outlined strokes so the segments can be animated (`pathLength="1"`).
- Motion values above come from the Figma Motion timelines.

## AI checklist

- [ ] Only for Login, App start, Logout
- [ ] Full-screen, centred, one loader
- [ ] Wordmark for Login/Logout, Progress loader for App start
- [ ] Never inside dialogs, lists or buttons
- [ ] Mark as reduced-motion fallback

## Open questions for the team

- **Timing values:** the ~400 ms threshold, ~1 s minimum and ~10 s message timing were suggested in the guidelines. Confirm them with development.

---

# Part 2 — Angular implementation

### API

```html
<pdr-brand-loader variant="mark|wordmark|progress" [value]="progress" />
```
Use only for app boot / full-page transitions. In-content loading → `../md3/progress-indicators.md` or skeletons.

Export SVGs with `download_assets` (MCP) into `assets/brand/`; animate with CSS, honor `prefers-reduced-motion` (static mark). `role="progressbar"` + `aria-label="PDR.cloud wird geladen"`; Progress variant binds `aria-valuenow`.
