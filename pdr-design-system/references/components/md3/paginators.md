# Paginators

Figma page: **Paginators** `3617:2525` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3617-2525)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Paginator** `8419:2279` — 40px high, gap 8, body-small

## Mapping
```html
<mat-paginator [length]="total" [pageSize]="25" [pageSizeOptions]="[10, 25, 50, 100]" showFirstLastButtons aria-label="Seiten" />
```
German labels: provide a `MatPaginatorIntl` subclass (`itemsPerPageLabel = 'Einträge pro Seite'`, `getRangeLabel` → "1–25 von 340").

## Overrides

None — Figma matches M3 defaults. Do not add any.
