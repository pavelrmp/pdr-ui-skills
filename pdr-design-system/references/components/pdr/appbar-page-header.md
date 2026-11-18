# Appbar & Page header

Figma page: **Appbar & Page header** `3330:116` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-116)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **App bar** `9329:6038` — `Version` v 2026 · `Size` Desktop|Tablet|Mobile (+ legacy **App bar mobile** `4104:21868`, **App bar tablet** `4104:21825`)
- **Top app bar** `5126:14156` — `Configuration` Small centered|Small|Medium|Large · `Elevation` flat|on-scroll
- **Page header** `10125:1535` — `Size` Desktop and Tablet|Mobile
- **Breadcrumbs** `3513:3670`, **Section title** `3317:94`, **Header actions** `8851:20492`, **Footer** `3642:7851`
- **Settings menu basic** `3558:2890`, **Second-level menu** `4798:1021`
- **Order title** `10917:39575`, **Suborders** `10917:39618`

## Mapping
| Figma | Wrapper | Built from |
|---|---|---|
| App bar (v 2026) | `<pdr-app-bar>` | `mat-toolbar`, `matIconButton` (menu, notifications with `matBadge`), `pdr-avatar` + `mat-menu` (account) |
| Size=Desktop/Tablet/Mobile | responsive inside `pdr-app-bar` via `BreakpointObserver` (M 768 / L 992) | — |
| Top app bar Small / Small centered / Medium / Large | `<pdr-top-app-bar size="small|center|medium|large">` | `mat-toolbar`; title: title-large (small) / headline-small (medium) / headline-medium (large) |
| Elevation=on-scroll | `[elevateOnScroll]="true"` → surface-container + level2 when scrolled (`CdkScrollable`) | — |
| Page header | `<pdr-page-header [title] [subtitle]>` with `pdrPageHeaderActions` slot | `headline-small`, `matButton`s |
| Breadcrumbs | `<pdr-breadcrumbs [items]>` | `<nav aria-label="Brotkrümel"><ol>` + `routerLink`, last item `aria-current="page"` |
| Section title | `<pdr-section-title>` | title-medium + optional action `matButton` |
| Header actions | `pdrPageHeaderActions` content | `matButton`, `matIconButton`, `mat-menu` |
| Settings menu / Second-level menu | `mat-menu` | see `../md3/menus-select.md` |
| Order title / Suborders | `<pdr-order-title>` | `mat-chip-listbox` for suborders |
| Footer | `<pdr-footer>` | body-small, on-surface-variant |

## Tokens
Background `--mat-sys-surface`, title `--mat-sys-on-surface`, icons `--mat-sys-on-surface-variant`, spacing `--pdr-space-16/24`.
