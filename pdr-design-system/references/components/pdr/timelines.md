# Timelines

Figma page: **Timelines** `3330:128` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-128)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Row activity** `8039:17166` — `Size` Widget|Changelog
- **History row** `10917:36536` — `State` Default|Hover · `Size` Mobile; **History row simple** `10917:40191`; **History table** `10917:36457`
- **Date** `5080:23687`, **Row** `5090:27491`, **Kundenkontakt** `4626:16593`

## API
```html
<pdr-timeline>
  <pdr-timeline-date [date]="day" />
  @for (e of events; track e.id) { <pdr-timeline-row [event]="e" size="widget|changelog" /> }
</pdr-timeline>
```
| Figma | Implementation |
|---|---|
| Row activity Widget / Changelog | `pdr-timeline-row size` — avatar + body-medium text + body-small time (on-surface-variant); vertical connector 1px `--mat-sys-outline-variant` |
| Date | sticky label-large separator |
| History row (+Hover) / simple / Mobile | `<pdr-history-row>` with state layer on hover; mobile stacks columns |
| History table | `mat-table` (see `../md3/data-grids.md`) |
| Kundenkontakt | `<pdr-contact-entry>` (channel icon + note) |

Semantics: `<ol>` list, times in `<time datetime>`.
