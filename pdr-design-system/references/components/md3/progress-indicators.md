# Progress indicators

Figma page: **Progress indicators** `10808:999` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10808-999)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Linear progress indicator** `10817:1121` — `Mode` Determinate|Buffer|Indeterminate|Query · `Value` 0|25|50|75|100|—
- **Circular progress indicator** `10817:1142` — `Mode` Determinate|Indeterminate · `Value` · `Size` 48|24

## Mapping
| Figma | Angular |
|---|---|
| Linear Mode=X | `<mat-progress-bar mode="determinate|buffer|indeterminate|query" [value] [bufferValue]>` |
| Circular Mode=X | `<mat-progress-spinner mode="determinate|indeterminate" [value]>` |
| Size=48 / 24 | `[diameter]="48"` / `[diameter]="24"` (inside buttons: 18) |

Always label: `aria-label="Wird geladen"` or `aria-labelledby`. Full-page/branded loading → `../pdr/brand-loader.md`; content placeholders → `../pdr/skeleton-empty-error-states.md`.

## Overrides

None — Figma matches M3 defaults. Do not add any.
