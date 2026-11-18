# Sliders

Figma page: **Sliders** `3617:2528` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3617-2528)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Slider MD3** `10696:43785` — `Version` slider_MD3_v1…v4
- **Slider handle** `10693:43661`, **Slider value handle** `10693:43664`, **Slider 3** `6816:1551`, **Slider right** `5804:19453`
- **Slider MD2** `10693:43630` — legacy, do not implement new usages

```html
<mat-slider min="0" max="100" step="5" discrete [showTickMarks]="true">
  <input matSliderThumb formControlName="value" />
</mat-slider>
```
## Mapping

Range → `<input matSliderStartThumb>` + `<input matSliderEndThumb>`. *Slider MD2* (`10693:43630`) is legacy — don't implement new usages.

| Figma | Angular |
|---|---|
| Slider value handle | `discrete` (value label on drag) |
| Tick marks | `[showTickMarks]="true"` + `step` |
| Disabled | `disabled` on `mat-slider` |

## Overrides

None — Figma matches M3 defaults. Do not add any.
