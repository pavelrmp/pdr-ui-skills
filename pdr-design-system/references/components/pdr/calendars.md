# Calendars

Figma page: **Calendars** `3330:110` · status 🌕 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-110)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

> 🌕 Not final in Figma. Use Material defaults / minimal styling and flag deviations in the PR.

## Components
- **Calendar header full-screen** `4968:3603` / **mobile** `4968:3611`
- **Gantt bar** `10917:32832` — `Property 1` Default|small
- **Vehicle in workshop** `10917:32801`

## Mapping
| Figma | Wrapper | Built from |
|---|---|---|
| Calendar header full-screen | `<pdr-calendar-header [view] [date]>` | `matIconButton` prev/next, `mat-button-toggle-group` (Tag/Woche/Monat), `matButton` "Heute" |
| Gantt bar | `<pdr-gantt-bar [start] [end] [status] size="default|small">` | absolutely positioned within planner grid; color from status → `--pdr-sys-*-container` |
| Vehicle in workshop | `<pdr-workshop-vehicle>` | `pdr-avatar` / car thumbnail + body-medium |

Planner grid columns reuse Data Grids column headers `Col Week / Col Day / Col Range` (`../md3/data-grids.md`). Drag to reschedule → `cdkDrag` with `cdkDragLockAxis="x"`.
