# Elevation

Figma: **⚛️ Design Tokens** page `3313:3` · [Elevation](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3420-434)
Machine-readable source: `../../tokens.json`. Theme setup: `../theming-rules.md`.

Figma effect styles `M3/Elevation Light/1–5` and `M3/Elevation Dark/1–5`. CSS: `--mat-sys-level0…5` (light/dark switch automatically through `--pdr-shadow-rgb`, see `../theming-rules.md`).

| Level | CSS | Light shadow | Dark shadow |
|---|---|---|---|
| level0 | `--mat-sys-level0` | `none` | `none` |
| level1 | `--mat-sys-level1` | `0 1px 2px 0px rgba(2, 6, 22,0.3), 0 1px 3px 1px rgba(2, 6, 22,0.15)` | `0 1px 2px 0px rgba(0, 0, 0,0.3), 0 1px 3px 1px rgba(0, 0, 0,0.15)` |
| level2 | `--mat-sys-level2` | `0 1px 2px 0px rgba(2, 6, 22,0.3), 0 2px 6px 2px rgba(2, 6, 22,0.15)` | `0 1px 2px 0px rgba(0, 0, 0,0.3), 0 2px 6px 2px rgba(0, 0, 0,0.15)` |
| level3 | `--mat-sys-level3` | `0 1px 3px 0px rgba(2, 6, 22,0.3), 0 4px 8px 3px rgba(2, 6, 22,0.15)` | `0 1px 3px 0px rgba(0, 0, 0,0.3), 0 4px 8px 3px rgba(0, 0, 0,0.15)` |
| level4 | `--mat-sys-level4` | `0 2px 3px 0px rgba(2, 6, 22,0.3), 0 6px 10px 4px rgba(2, 6, 22,0.15)` | `0 2px 3px 0px rgba(0, 0, 0,0.3), 0 6px 10px 4px rgba(0, 0, 0,0.15)` |
| level5 | `--mat-sys-level5` | `0 4px 4px 0px rgba(2, 6, 22,0.3), 0 8px 12px 6px rgba(2, 6, 22,0.15)` | `0 4px 4px 0px rgba(0, 0, 0,0.3), 0 8px 12px 6px rgba(0, 0, 0,0.15)` |

Shadow color: `sys/shadow` = `#020616` (light) / `#000000` (dark).

## Where each level is used

| Level | Components |
|---|---|
| 0 | Page content, panels, filled and outlined cards, tables |
| 1 | **App bar (locked)**, elevated cards, elevated chips, bottom sheet |
| 2 | Menus, autocomplete panel, rich tooltip, tipseens |
| 3 | FAB, side sheets, popovers, snackbar |
| 4 | Dragged items (`cdkDragPreview`) |
| 5 | Dialogs |

## Rules

1. Use `box-shadow: var(--mat-sys-levelN)` or the component’s elevation token — never a custom shadow.
2. Elevation separates layers; don’t use it as decoration. Panels separate from the page by color (`surface-container-lowest` on `surface`), not by shadow.
3. Figma components use the light styles; dark mode gets the dark shadow automatically in code.
