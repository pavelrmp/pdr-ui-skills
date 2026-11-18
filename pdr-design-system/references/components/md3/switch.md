# Switch

Figma page: **Switch** `3617:2527` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3617-2527)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Switch** `4352:16437` — `State` Enabled|Hovered|Focused|Pressed|Disabled · `Icon` No|Yes · `Checked` Yes|No · 52×32, track primary
- **Form switcher** `4352:17495` — `Position` Left|Right

## Mapping
| Figma | Angular |
|---|---|
| Switch | `<mat-slide-toggle formControlName="x">Label</mat-slide-toggle>` |
| Checked=Yes | control value `true` |
| Icon=No | `hideIcon` |
| Icon=Yes | default |
| Form switcher Position=Left / Right | `labelPosition="after"` / `labelPosition="before"` |
| State=Disabled | `control.disable()` |

## Overrides

None — Figma matches M3 defaults. Do not add any.
