# Status tags

Figma page: **Status tags** `3346:263` · status 🌕 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3346-263)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

> 🌕 Not final in Figma. Use Material defaults / minimal styling and flag deviations in the PR.

## Components
- **Status** `3603:201` — `Size` Text|Icon + Text|Icon · `Status` Success|Error|Warning|Info|Neutral
- **Employee status** `4510:21042` — `Status` Working|Sick|On vacation|On break|Off duty|Not clocked in|Short-time work|Flextime
- **Process status** `4487:13151` — `Status` Kunde kontaktieren|Schaden erfasst|Fahrzeug kommt|Abgeschlossen|In Reparatur|Wartet auf Reparatur|Warte auf Besichtigung|KV erstellen
- **Appointment** `10286:5503` — `Status` Besichtigung|Reparaturende|Reparaturstart|Bringen|Holen|Anlieferung|Auslieferung
- **Delivery status** `9777:8457` — `Color` Yellow|Grey|Green|Blue · `Flow` · `State`; **Check status** `9777:8494` — `Color` Yellow|Green|AI
- **Price chip** `9777:8538` — `State` Enabled|Hovered|Focused|Pressed|Updated
- **Repair status** `4657:36242` — `Status` Default|Planned|Done · `Step` Painting|Bodywork|Electrical|Hail damage|Mechanics|Paint preparation|Final inspection|Wheel alignment
- **Premium feature** `7691:16037`, **Pie chart** `4418:13085`

## Base: `pdr-status-tag`
24h, `corner-small`, padding 2/8 (`--pdr-space-2` / `--pdr-space-8`), gap 4, `--mat-sys-label-large`.
```html
<pdr-status-tag status="success" display="icon-text">Abgeschlossen</pdr-status-tag>
```
| Figma Size | `display` |
|---|---|
| Text | `"text"` |
| Icon + Text | `"icon-text"` |
| Icon | `"icon"` (requires `aria-label`) |

| Status | background | text/icon |
|---|---|---|
| success | `--pdr-sys-success-container` | `--pdr-sys-on-success-container` |
| error | `--mat-sys-error-container` | `--mat-sys-on-error-container` |
| warning | `--pdr-sys-warning-container` | `--pdr-sys-on-warning-container` |
| info | `--pdr-sys-info-container` | `--pdr-sys-on-info-container` |
| neutral | `--mat-sys-surface-container-high` | `--mat-sys-on-surface-variant` |
| extended (domain) | `--pdr-sys-{orange,amber,lime,emerald,teal,pink,purple,cyan,indigo}-container` | `--pdr-sys-on-…-container` |

## Domain tags (thin wrappers that map an enum → status/color + icon)
| Figma | Wrapper |
|---|---|
| Employee status | `<pdr-employee-status [status]="EmployeeStatus">` |
| Process status | `<pdr-process-status [status]="ProcessStatus">` |
| Appointment | `<pdr-appointment-tag [type]="AppointmentType">` |
| Delivery status | `<pdr-delivery-status [color] [flow]>` (interactive → `button` with state layer) |
| Check status | `<pdr-check-status [state]="'yellow'|'green'|'ai'">` |
| Repair status | `<pdr-repair-status [step] [status]="'default'|'planned'|'done'">` |
| Price chip | `<pdr-price-chip [amount] [updated]>` (State=Updated → `--pdr-sys-warning-container` highlight) |
| Premium feature | `<pdr-premium-badge>` (`--mat-sys-tertiary-container`) |

Keep each enum → color mapping in one `*.status-map.ts`; read exact color per Figma variant via MCP `get_variable_defs` before adding entries. Color must never be the only signal — always text or `aria-label`.
