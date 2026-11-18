# Button toggle (Segmented buttons)

Figma page: **Button toggle (Segmented buttons)** `3330:91` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-91)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Segmented button** `5099:11600` — `Segments` 2|3|4|5|6
- **Button segment** (start `5097:4335` / middle `5097:4461` / end `5097:4587`) — `Configuration` Label only|Label & icon|Icon only · `State` Enabled|Hovered|Focused|Pressed|Disabled · `Selected` True|False
- `Example/Segmented button` `10723:15638` (use cases: Arrows, View list/cards, Status filtering, Time range, View selection, Car view, Filtering) — reference only

## Mapping
| Figma | Angular |
|---|---|
| Segmented button | `<mat-button-toggle-group [hideSingleSelectionIndicator]="false" aria-label="…">` |
| Segment | `<mat-button-toggle value="…">` (start/middle/end shapes are automatic) |
| Segments=N | N toggles |
| Selected=True | group `[(value)]` / `formControlName` |
| Configuration=Label & icon | `<mat-icon fontSet="material-symbols-outlined">` + text |
| Configuration=Icon only | icon + `aria-label` on the toggle |
| State=Disabled | `disabled` on toggle or group |
| Use case Filtering / Status filtering | `multiple` |

```html
<mat-button-toggle-group [(value)]="view" aria-label="Ansicht">
  <mat-button-toggle value="list"><mat-icon fontSet="material-symbols-outlined">list</mat-icon>Liste</mat-button-toggle>
  <mat-button-toggle value="cards">Karten</mat-button-toggle>
</mat-button-toggle-group>
```
Use case **Arrows** (prev/next) is not a toggle → two `matIconButton`s with `pdr-icon-btn--outlined`.

## Overrides

None — Figma matches M3 defaults. Do not add any.
