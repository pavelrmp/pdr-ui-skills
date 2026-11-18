# Snackbar

Figma page: **Snackbar** `10745:46606` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10745-46606)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Snackbar** `8028:8446` — `Configuration` Text only|Text & action|Text & longer action · lines One|Two · `Show close affordance` · inverse-surface, `corner-extra-small`, level3, body-medium

## Mapping
| Figma | Angular |
|---|---|
| Text only | `snackBar.open('Gespeichert', undefined, { duration: 4000, panelClass: 'pdr-snackbar' })` |
| Text & action | `snackBar.open('Gelöscht', 'Rückgängig', { duration: 6000, panelClass: 'pdr-snackbar' })` |
| Longer action / two lines / close affordance | `snackBar.openFromComponent(PdrSnackbar, { data: { message, action, closable: true }, panelClass: 'pdr-snackbar' })` |

`PdrSnackbar` uses `matSnackBarLabel`, `matSnackBarActions`, `matSnackBarAction` directives and a close `matIconButton`. Position defaults to bottom-center.


Never use snackbars for errors that need action — use `../pdr/alerts.md`.

## Overrides

None — Figma matches M3 defaults. Do not add any.
