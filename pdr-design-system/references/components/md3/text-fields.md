# Text fields

Figma page: **Text fields** `3330:98` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-98)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

Rules: always Reactive Forms; errors via `<mat-error>`; supporting text via `<mat-hint>`; label is `<mat-label>`, never a placeholder.

## Components
- **Text field** `3422:580` — `Style` Outlined|Filled|Transparent BG · `State` Enabled|Focused|Error|Disabled|Hovered · `Text configurations` Input|Label|Placeholder · 56px, `corner-extra-small`, body-large
- **Text area** `5518:85321` — `Style` Outlined|Filled · `State`
- **Supporting text** `3422:540`, **Quick text input** `6447:4565`, **Drag indicator** `9119:5561`
- **Search bar** `4470:1363` — `State` · `Show avatar`; **Search view full-screen** `4545:24986`; **Search result** `4545:27265`
- **Code input** `3443:103` / **Code input cell** `3434:363` — `State` Enabled|Focused|Filled|Error|Disabled|Hovered

## Mapping — Text field
| Figma | Angular |
|---|---|
| Style=Outlined | `<mat-form-field appearance="outline">` |
| Style=Filled | `<mat-form-field appearance="fill">` |
| Style=Transparent BG | `appearance="fill"` + `class="pdr-field--transparent"` |
| State=Error | validator + `<mat-error>`; never force with CSS |
| State=Disabled | `control.disable()` (not the `disabled` attribute with reactive forms) |
| Supporting text | `<mat-hint>` (`align="end"` for counters) |
| Leading / trailing icon | `<mat-icon matPrefix>` / `<mat-icon matSuffix>`; clear button = `<button matIconButton matSuffix>` |

```html
<mat-form-field appearance="outline">
  <mat-label>Kennzeichen</mat-label>
  <input matInput formControlName="plate" />
  <mat-hint>z. B. B-AB 1234</mat-hint>
  @if (form.controls.plate.hasError('required')) { <mat-error>Pflichtfeld</mat-error> }
</mat-form-field>
```

## Text area

`<textarea matInput cdkTextareaAutosize cdkAutosizeMinRows="3">` in the same form field.
## Search bar / Search view
No Material equivalent. `<pdr-search-bar [avatar]>`: 56px, `corner-extra-large`, `surface-container-lowest`, gap 4, body-large; results via `mat-autocomplete`. Full-screen view on mobile → `MatDialog` full-screen (see `dialogs.md`).

## Code input — `3443:103`
`<pdr-code-input [length]="6" formControlName="otp">`. Implements `ControlValueAccessor`; each cell reuses outline field tokens (`outline`, `corner-extra-small`), states Enabled|Focused|Filled|Error|Disabled. Use `autocomplete="one-time-code"` and `inputmode="numeric"`.

## Quick text input
Inline single-line add (e.g. new note) → borderless `matInput` in `appearance="fill"` + `pdr-field--transparent`, submit with `matIconButton` suffix.

## Overrides (`styles/components/md3/_text-fields.scss`)
```scss
@use '@angular/material' as mat;
// Figma Style=Transparent BG (also Dropdown Style=Standard)
.pdr-field--transparent { @include mat.form-field-overrides((filled-container-color: transparent)); }
```
Heights, outline color and radius = M3 defaults.
