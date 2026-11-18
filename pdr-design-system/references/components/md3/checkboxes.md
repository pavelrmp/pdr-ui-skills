# Checkboxes

Figma page: **Checkboxes** `3617:2526` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3617-2526)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Checkbox** `4091:9260` — `State` Enabled|Hovered|Focused|Pressed|Disabled · `Select` Selected|Unselected|Indetermined · 48px target
- **Checkbox with label** `4091:9478`

## Mapping
| Figma | Angular |
|---|---|
| Select=Selected / Unselected | `[checked]` or `formControlName` |
| Select=Indetermined | `[indeterminate]="true"` (e.g. "select all" with partial selection) |
| State=Disabled | `control.disable()` / `[disabled]` |
| Checkbox with label | `<mat-checkbox>Label</mat-checkbox>`; label before → `labelPosition="before"` |
| Table row selection | see `data-grids.md` (`SelectionModel`) |

## Overrides

None — Figma matches M3 defaults. Do not add any.
