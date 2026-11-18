# Filters

Figma: **Filters_example** `10798:15767` · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10798-15767) — reference for every filter bar.
Components: `../components/md3/chips.md`, `../components/pdr/toolbars-pdr.md` (`pdr-filter-bar`).

## Patterns in the example
| Pattern | Layout | Use |
|---|---|---|
| **Filter** (`3617:5043`) | panel: surface-container-lowest, corner-large, pad 16, gap 24, 80 px; left: search + selects; right container: actions (gap 8) | Default list filter |
| **Filter chips** | row of Filtering chip v2 + Dropdown chips, 48 px, gap 8 | Inside a data-grid panel (`data-grid-page.md`) |
| **Invoice filter** (`4418:6537`) | 73 px bar with status filters | Payment & invoices |
| **Task filter** (`5192:41171`) | compact 32 px chip row, gap 4 | To-do lists |
| **Filter Analytics** | panel 56 px, gap 24 | Dashboards: date range + dimensions |
| Info alert above filters | `pdr-alert type="info"`, full width | Explain a filtered / limited view |

## Rules
- Filters sit **above** the content they affect, inside the same panel when they filter a single table.
- Active filters are visible as selected chips; always offer "Filter zurücksetzen" (text button) when any filter is active.
- Multi-value filters → Dropdown chip opening a `mat-menu` with checkboxes; date range → `mat-date-range-input`.
- Persist filters in URL query params (`queryParamsHandling: 'merge'`) so views are shareable and survive reload.
- Mobile: one horizontally scrollable chip row (`pdr-chip-set--scroll`); advanced filters in a bottom sheet.
