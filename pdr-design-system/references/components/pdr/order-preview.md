# Order preview

Figma page: **Order preview** `4546:19307` · status 🌕 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=4546-19307)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

> 🌕 Not final in Figma. Use Material defaults / minimal styling and flag deviations in the PR.

## Components
- **Order card S** `5266:9622` — `Status` done|open|in repair; **Order card M** `5109:7717`; **Order card v2** `8560:12304`
- **Order popover** `10735:44174` / **v2** `10735:43867` — `Breakpoint` Desktop and Tablet|Mobile; **Order popover v1** `4911:4142`
- **Workshop status** `10735:43959` — `Status` Default|Abgeschlossen|Finish|Lackvorbereitung; **compact** `10735:43868`
- **Order link chip** `9113:13847`, **Order not attached** `9119:2621` — `Order` Not attached|Attached
- **Car info** `10917:33183`, **Order customer info** `10917:33245`, **Order info** `5123:7259`, **Chat order info** `6714:14709`
- **Replacement vehicle** `5290:10137`, **Employee row** `10917:33339`, **Stepper v1** `10917:33303`, **To-do card** `10917:33034`
- **Order preview toolbar** `10917:33502`, **Orders overview** `10917:33738`

## Mapping
| Figma | Wrapper | Built from |
|---|---|---|
| Order card S / M / v2 | `<pdr-order-card [order] size="s|m">` | `mat-card appearance="outlined"`, `pdr-status-tag`, `pdr-avatar` |
| Status done/open/in repair | `pdr-status-tag` (success / info / warning) | see `status-tags.md` |
| Order popover (+Mobile) | `<pdr-order-popover>` | desktop: `cdkConnectedOverlay` (surface-container-lowest, `corner-large`, level3); mobile: `MatBottomSheet` |
| Workshop status (+compact) | `<pdr-workshop-status [status] [compact]>` | `pdr-process-status` + `mat-progress-bar` |
| Order link chip | `<pdr-order-link-chip>` | `mat-chip` + `routerLink` |
| Order not attached | `<pdr-order-attach>` | outlined `matButton` "Auftrag zuordnen" / attached `pdr-order-link-chip` |
| Car info / Order customer info / Order info | `<pdr-car-info>`, `<pdr-customer-info>`, `<pdr-order-info>` | definition lists (`dl`), label-medium labels + body-medium values |
| Replacement vehicle | `<pdr-replacement-vehicle>` | `mat-card` |
| Employee row | `<pdr-employee-row>` | `mat-list-item` + `pdr-avatar` + `pdr-employee-status` |
| Stepper v1 | `pdr-wizard-steps` | see `workflows.md` |
| Order preview toolbar | `<pdr-order-toolbar>` | see `toolbars-pdr.md` |
