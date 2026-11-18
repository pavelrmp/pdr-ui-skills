# Navigation drawer & rail

Figma page: **Navigation drawer & rail** `10826:961` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10826-961)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Navigation drawer** `9235:8209` — `Type` Side Nav medium|Side Nav Expanded (Vorgänge, Lager, Finanzen, Verwaltung, Analytics, Docs, Sonstiges)
- **Navigation drawer item** `4083:7759` — `State` Enabled|Hovered|Pressed|Selected · `Level` 1st|2nd · 56px, `corner-full`

PDR app navigation (badges, banners, mobile drawer) lives in `../pdr/navigation-menu.md`; this file is the Material layer underneath.

## Mapping
| Figma | Angular |
|---|---|
| Navigation drawer | `<mat-sidenav-container>` + `<mat-sidenav [mode]="isDesktop ? 'side' : 'over'" [opened]>` |
| Side Nav medium (rail) | `pdr-sidenav--rail` (collapsed width, icons only + `matTooltip`) |
| Navigation drawer item Level 1st | `<a mat-list-item routerLink routerLinkActive #rla="routerLinkActive" [activated]="rla.isActive">` in `<mat-nav-list>` |
| Level 2nd | same + `class="pdr-nav-item--nested"` |
| State=Selected | `[activated]` (secondary-container) + `aria-current="page"` |
| Section labels | `<div mat-subheader>` |

## Overrides (`styles/components/md3/_navigation-drawer.scss`)
```scss
@use '@angular/material' as mat;
.pdr-sidenav {
  // Figma drawer item: 56px, fully rounded
  @include mat.list-overrides((
    list-item-one-line-container-height: 56px,
    active-indicator-shape: var(--mat-sys-corner-full),
    active-indicator-color: var(--mat-sys-secondary-container),
  ));
}
.pdr-nav-item--nested { padding-inline-start: var(--pdr-space-48); }
```
