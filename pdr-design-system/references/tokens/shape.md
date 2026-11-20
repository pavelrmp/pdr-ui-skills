# Shape (corner radius)

Figma: **⚛️ Design Tokens** page `3313:3` · [Design Tokens page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3313-3)
Machine-readable source: `../../tokens.json`. Theme setup: `../theming-rules.md`.

Figma collection `Corner radius` (7 values). CSS: `--mat-sys-corner-*`. Values equal the M3 defaults.

| Token | Figma | Value | CSS |
|---|---|---|---|
| none | None | 0 | `--mat-sys-corner-none` |
| extra-small | xs | 4 px | `--mat-sys-corner-extra-small` |
| small | s | 8 px | `--mat-sys-corner-small` |
| medium | m | 12 px | `--mat-sys-corner-medium` |
| large | l | 16 px | `--mat-sys-corner-large` |
| extra-large | xl | 28 px | `--mat-sys-corner-extra-large` |
| full | Full | 9999 px (Figma 1000) | `--mat-sys-corner-full` |

## Where each radius is used

| Radius | Components |
|---|---|
| extra-small (4) | Text fields, select, menus, autocomplete panel, snackbar, plain tooltip, alerts |
| small (8) | Chips, status tags |
| medium (12) | Cards, rich tooltip, megaoptions |
| large (16) | **Panels**, side sheets (start corners), FAB, mobile dialogs, toolbar |
| extra-large (28) | Dialogs (desktop/tablet), bottom sheet (top corners), search bar |
| full | Buttons, icon buttons, badges, avatars, nav drawer items, switch track |
| none | Tables (never rounded), full-screen dialogs |

Rule: never hard-code a radius; use the token of the component’s shape role above.
