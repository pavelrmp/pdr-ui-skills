# Alerts

Figma page: **Alerts** `3330:109` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-109)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Alert filled** `3393:4752` — `Message` Warning|Info|Success|Error · `Style` Standard|Longer action · 320w, `corner-extra-small`, title-medium
- **Register device card** `10917:32523` — `Main action` CTA|Registered

## API
```html
<pdr-alert type="warning" layout="inline" [dismissible]="true">
  <span pdrAlertTitle>Prüfung ausstehend</span>
  Bitte Rechnung prüfen.
  <button matButton pdrAlertAction>Prüfen</button>
</pdr-alert>
```
| Figma | Input |
|---|---|
| Message=Warning/Info/Success/Error | `type="warning|info|success|error"` |
| Style=Standard | `layout="inline"` (action right) |
| Style=Longer action | `layout="stacked"` (action below text) |

## Tokens
| type | background | text / icon | icon |
|---|---|---|---|
| warning | `--pdr-sys-warning-container` | `--pdr-sys-on-warning-container` | `warning` |
| info | `--pdr-sys-info-container` | `--pdr-sys-on-info-container` | `info` |
| success | `--pdr-sys-success-container` | `--pdr-sys-on-success-container` | `check_circle` |
| error | `--mat-sys-error-container` | `--mat-sys-on-error-container` | `error` |

Radius `--mat-sys-corner-extra-small`, padding 12/16, gap 12, title `--mat-sys-title-medium`, body `--mat-sys-body-medium`.

## A11y
`role="alert"` for error/warning raised by user action, `role="status"` otherwise. Dismiss button: `matIconButton` with `aria-label="Schließen"`.

## Register device card
`<pdr-register-device-card [registered]>` — `mat-card appearance="outlined"` + filled `matButton` (CTA) or success `pdr-status-tag` (Registered).
