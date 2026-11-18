# Radio buttons

Figma page: **Radio buttons** `3453:2024` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3453-2024)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Radio buttons** `5365:17885` — `Selected` True|False · `State` Enabled|Hovered|Focused|Pressed|Disabled

## Mapping
| Figma | Angular |
|---|---|
| Group | `<mat-radio-group formControlName="x" aria-label="…">` |
| Radio | `<mat-radio-button value="a">Label</mat-radio-button>` |
| Selected=True | group value |
| State=Disabled | `disabled` on button or group |

Large tile-style choices → `../pdr/megaoptions-todo.md` (Megaoption).

## Overrides

None — Figma matches M3 defaults. Do not add any.
