# Pickers

Figma page: **Pickers** `10850:42483` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10850-42483)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Color sample** `5569:34106` — `State` Enabled|Selected; **Palette 1** `5569:34105`, **Palette 2** `5569:32134`
- **Touchspin** `10133:12467`
- **Date range picker (Matero)** `8669:6184`

## Mapping
| Figma | Wrapper | Built from |
|---|---|---|
| Palette 1/2 + Color sample | `<pdr-color-picker formControlName [palette]>` | `role="radiogroup"`; each swatch `role="radio"` 32px `corner-full`; Selected → check icon + 2px `--mat-sys-on-surface` ring. Palette values = `ref.palette.*` tones from tokens.json |
| Touchspin | `<pdr-touchspin formControlName [min] [max] [step]>` | `matIconButton` (−/+) around `matInput type="number"` (outline); `ControlValueAccessor`; arrow keys step |
| Date range picker (Matero) | use `mat-date-range-input` + `mat-date-range-picker` with preset panel (`pdr-date-range-presets`, `matDateRangePickerActions`) | see `../md3/date-time-pickers.md` |
