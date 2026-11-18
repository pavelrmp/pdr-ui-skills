# Toolbar

Figma page: **Toolbar** `10826:962` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10826-962)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Toolbar** `3617:2745` — 88h, surface-container-lowest, `corner-large`, padding 16, gap 10

## Mapping
| Figma | Angular |
|---|---|
| Toolbar | `<mat-toolbar class="pdr-toolbar">` with projected `matButton` / `matIconButton` / `mat-form-field` |
| Spacer between groups | `<span class="pdr-spacer"></span>` |

Domain toolbars (order, filters) → `../pdr/toolbars-pdr.md`.

## Overrides (`styles/components/md3/_toolbar.scss`)
```scss
@use '@angular/material' as mat;
.pdr-toolbar {
  @include mat.toolbar-overrides((
    container-background-color: var(--mat-sys-surface-container-lowest),
    standard-height: 88px,
  ));
  border-radius: var(--mat-sys-corner-large);
  padding: var(--pdr-space-16);
  gap: var(--pdr-space-8);
}
```
