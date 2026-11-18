# Brand loader

Figma page: **Brand loader** `10826:963` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10826-963)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Brand loader/Mark** `10798:21798`, **Brand loader/Progress loader** `10798:21785`, **Brand loader/Wordmark** `10798:21822`

## API
```html
<pdr-brand-loader variant="mark|wordmark|progress" [value]="progress" />
```
Use only for app boot / full-page transitions. In-content loading → `../md3/progress-indicators.md` or skeletons.

Export SVGs with `download_assets` (MCP) into `assets/brand/`; animate with CSS, honor `prefers-reduced-motion` (static mark). `role="progressbar"` + `aria-label="PDR.cloud wird geladen"`; Progress variant binds `aria-valuenow`.
