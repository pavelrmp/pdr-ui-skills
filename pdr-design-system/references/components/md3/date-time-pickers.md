# Date & time pickers

Figma page: **Date & time pickers** `3330:122` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-122)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Docked date picker** `8663:35194` — `Type` Day|Month|Year
- **Modal date picker** `8663:35336` — `Type` Day|Year|Full-screen (range)
- **Input date picker** `8663:35307` — `Type` Single input|Range
- **Day cell** `6667:6795`, **Date range calendar** `4099:8960`, **Single date picker** `8662:8678`
- **Keyboard picker** `8663:36037` — `Format` 12 hour|24 hour
- **Dial picker** `8663:35976` — `Format` · `Orientation` Vertical|Horizontal

## Mapping
| Figma | Angular |
|---|---|
| Docked date picker | `<input matInput [matDatepicker]="dp">` + `<mat-datepicker-toggle matIconSuffix [for]="dp">` + `<mat-datepicker #dp>` |
| Modal date picker | same + `<mat-datepicker touchUi>` |
| Input date picker / Range | `<mat-date-range-input [rangePicker]="rp">` with `matStartDate` / `matEndDate` + `<mat-date-range-picker #rp>` |
| Keyboard (time) picker | `<input matInput [matTimepicker]="tp">` + `<mat-timepicker #tp>` |
| Dial picker | `<pdr-time-dial>` (no Material equivalent) |
| 12 / 24 hour | driven by locale (`MAT_DATE_LOCALE`, default `de-DE` → 24h) |
| Docked Type=Month/Year | `startView="multi-year"` / `"year"` |
| Modal Full-screen (range) | `<mat-date-range-picker touchUi>` |

Use `provideDateFnsAdapter()` (or the project adapter); never format dates in templates manually. Date range picker (Matero) on Pickers page → see `../pdr/pickers.md`.

## Overrides

None — Figma matches M3 defaults. Do not add any.
