# Sheets

Figma page: **Sheets** `5197:5440` · status 🌕 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=5197-5440)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

> 🌕 Not final in Figma. Use Material defaults / minimal styling and flag deviations in the PR.

## Components
- **Side Sheet** `8161:21398` — 500w, surface-variant, start corners `corner-large`, level3
- `Example/Side sheet` `10850:38434` (Summary, Forms 1/2, Timeline), `Example/Order planning` `10557:5619` — reference only

## Mapping
| Figma | Angular |
|---|---|
| Side Sheet `8161:21398` (500w) | Route-level: `<mat-sidenav position="end" mode="over">` inside `mat-sidenav-container`. Programmatic: `<pdr-side-sheet>` opened via `MatDialog` with `position: { right: '0' }`, `height: '100dvh'`, `panelClass: ['pdr-dialog', 'pdr-side-sheet']` |
| Bottom sheet (mobile) | `MatBottomSheet.open(Component, { panelClass: 'pdr-bottom-sheet' })` |

Side sheet tokens: surface-variant, start corners `corner-large`, level3.


## Overrides (`styles/components/md3/_sheets.scss`)
```scss
@use '@angular/material' as mat;
.pdr-side-sheet {
  @include mat.dialog-overrides((
    container-color: var(--mat-sys-surface-variant),
    container-shape: var(--mat-sys-corner-large) 0 0 var(--mat-sys-corner-large),
    container-elevation-shadow: var(--mat-sys-level3),
  ));
}
```
