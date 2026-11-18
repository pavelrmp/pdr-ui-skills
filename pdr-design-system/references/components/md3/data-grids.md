# Data Grids

Figma page: **Data Grids** `3330:114` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-114)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Column header** `3562:4059` — `Type` Col Left|Col center|Col right|Checkbox|Col Week|Col Day 1|Col Day 2|Col Range
- **Cell one line** `3562:4020` — `Type` Text|Text + Caption|Icon|Icon+Text|Avatar+Name|Avatar+Text+Caption|GroupofAvatars|Status|ProgressBar|StepsComplete|Switcher|Input|Dropdown Chip|Actions|Kebab menu|Chart|Time|Cell Text Center Date|Visa ***123
- **Cell 2+ lines** `10702:50291` — `Type` Text|Text 2 Lines|Customer|Order|ToDo|Status|Checkbox|Avatar|Action|Dropdown|Date 1|Group|Col header
- **Cell input** `8822:15188` — `Filled` Default|Filled · `State`
- **Table footer** `3562:4052` — `Type` Subtotal|Total

## Mapping
| Figma | Angular |
|---|---|
| Table | `<table mat-table [dataSource] matSort>` (+ `MatPaginator`, see `paginators.md`) |
| Column header Col Left/center/right | `<th mat-header-cell mat-sort-header>` + `pdr-col--start|center|end` (numbers right-aligned) |
| Column header Checkbox / Cell Checkbox | `SelectionModel` + `<mat-checkbox>` (master uses `[indeterminate]`) |
| Cell Text / Text + Caption / 2 lines | `<td mat-cell>` + `<pdr-cell-text [caption]>` |
| Cell Avatar+Name / Customer / GroupofAvatars | `<pdr-avatar>` / `<pdr-avatar-group>` in cell |
| Cell Status | `<pdr-status-tag>` (see `../pdr/status-tags.md`) |
| Cell ProgressBar | `<mat-progress-bar mode="determinate">` |
| Cell Switcher | `<mat-slide-toggle>` |
| Cell Input / Cell input | `<pdr-cell-input>` (borderless `matInput`, states via tokens) |
| Cell Dropdown Chip | `<pdr-dropdown-chip>` |
| Cell Actions / Kebab menu | `matIconButton` + `[matMenuTriggerFor]` |
| Col Week/Day/Range | planner grids → `../pdr/calendars.md` |
| Table footer Subtotal/Total | `*matFooterRowDef` + `<td mat-footer-cell>` (title-small) |

Rules: sticky header `*matHeaderRowDef="cols; sticky: true"`; row click → `(click)` on `tr` + `role="link"` + keyboard handler; empty/loading rows → `*matNoDataRow` with `<pdr-empty-state>` / `<pdr-skeleton-table-row>`.

## Key principles (Figma: "Data grid · Key principles", `10684:43362`, `10937:3494`, `10937:3504`, `10937:3514`, `10937:3524`)

Before laying out a table, analyse the content: what users search for, compare and select by, and how they move through rows and columns. These rules are mandatory for every `mat-table`.

### Improving a table
1. **Keep only the data that matters.** Show only columns used to search, compare or select a row. Internal IDs, postcode, colour etc. go to the detail page.
2. **Order columns for comparison.** Values that are compared (Netto · MwSt. · Brutto) sit next to each other.
3. **Combine related columns.** Make + model + plate → one two-line cell (`pdr-cell-text` with caption) instead of three narrow columns.
4. **Key field first.** The identifying field (e.g. order number) is the first column and may be emphasised (`--mat-sys-title-small` / bold).
5. **Show data as icons, tags or statuses.** Replace yes/no or enum columns with `pdr-status-tag` / icons that can be scanned at a glance.
6. **De-emphasise secondary data** with `--mat-sys-on-surface-variant`, used sparingly — most text stays `--mat-sys-on-surface`. Never grey out everything.
7. **No outline, no rounded corners.** A table never has its own border or radius; it sits flush in its container. Structure comes from the header divider, alignment and spacing. It may sit inside a `pdr-panel` (`surface-container-lowest`, no border). Applies on desktop and mobile.

### Header
- **Omit the header** for simple, self-explanatory tables (e.g. a short two-column list).
- **Align column titles like their cells** — numeric columns have right-aligned titles.
- **2 px divider** under the header in `--mat-sys-outline-variant`; no header background.
- **Header text** in `--mat-sys-on-surface`; secondary info (units) in `--mat-sys-on-surface-variant`. No blue or uppercase titles.
- **Select-all, sort and filter live in the header** (master checkbox, `mat-sort-header`, filter icon) — not as separate buttons above the table.
- **Abbreviations** in titles (SD, WS, INS, DG, GLM, GL, H+B, KV, MW, RW, REP…) always get a `matTooltip` with the full term.
- **Sticky header** (`*matHeaderRowDef="cols; sticky: true"`) when it helps users keep orientation and keeps sort/filter reachable.

### Content
- **Row dividers are optional** (`--mat-sys-outline-variant`, 1 px) — only if the table falls apart without them. Never on the last row. Never a full cell grid.
- **Alignment:** text left; numbers right with tabular (monospaced) digits (`font-variant-numeric: tabular-nums`) and thousands grouping (`DecimalPipe` / `CurrencyPipe`, `de-DE`). Header of numeric columns right-aligned too.
- **Top-align cells to the first-line baseline** (`vertical-align: top`, consistent cell padding 12/8) — never vertically centre multi-line rows.
- **Row hover:** whole row gets an `on-surface` 8 % state layer (`--pdr-state-layer-on-surface-8`). One row at a time; never change text colour/weight. Pointer devices only (`@media (hover: hover)`).
- **Selected rows** (via checkbox) get `--mat-sys-primary-container`. Show the selection count and bulk actions in a toolbar above the table.
- **Clickable cells become links on row hover:** at rest they look like plain `on-surface` text; in the hovered row they turn `--mat-sys-primary`, and the cell under the pointer is underlined with `cursor: pointer`. Never make all clickable cells blue at rest.

### Footer
- **Only when it adds information** (totals, subtotals, pagination).
- **Totals align with their column:** label ("Summe", "Zwischensumme") in the first column, left-aligned; values right-aligned with tabular digits.
- **Emphasise the total, not the subtotal:** Subtotal `--mat-sys-body-large` + `on-surface-variant`; Total `--mat-sys-title-medium` + `on-surface`. No colour highlighting.
- **1 px `outline-variant` divider above the footer**; same background as rows.
- **Pagination below the table**, right-aligned `<mat-paginator>` with 10 / 25 / 50 / 100. Paginate from 50 rows; infinite scroll only for feeds.
- **Sticky footer** (`*matFooterRowDef="cols; sticky: true"`) when the table scrolls inside its container. No actions in the footer — bulk actions belong in the toolbar above.

### Mobile (< 600 px, `Breakpoints.Handset`)
- **Don't shrink the desktop table.** Switch template with `BreakpointObserver`: `≥ 600 px → <table mat-table>`, `< 600 px → <mat-list>` (or cards). Never one template for all widths.
- **List item anatomy:** headline = key field; supporting text = 1–2 secondary values (`K. Karo · Mercedes-Benz A-Klasse`); trailing = status tag or amount. Everything else lives on the detail page.
- **Whole row is the touch target** (≥ 48 × 48 px), opens the detail view; nothing depends on hover. Secondary actions in a trailing `more_vert` `mat-menu`.
- **Controls move out of the header:** sorting → menu/bottom sheet, filters → horizontally scrollable filter chips (`pdr-chip-set--scroll`), selection → long-press + contextual top app bar.
- **Horizontal scroll only to compare** (e.g. calculations): freeze the first column (`sticky` column def) and show a visible cut-off edge.
- **Sizing:** 16 px side padding (`--pdr-space-16`); row height 56 / 72 / 88 px for 1 / 2 / 3 lines; primary text `body-large` + `on-surface`, secondary `body-medium` + `on-surface-variant`.
- **"Mehr laden" or infinite scroll** (with progress indicator) instead of the paginator; totals in a sticky summary bar at the bottom.
- **Loading / empty:** `pdr-skeleton-list-item` while loading, `pdr-empty-state` when empty. Never show an empty table header.

```ts
isHandset = toSignal(inject(BreakpointObserver).observe(Breakpoints.Handset).pipe(map(r => r.matches)), { initialValue: false });
```
```html
@if (isHandset()) {
  <mat-nav-list>
    @for (o of orders(); track o.id) {
      <a mat-list-item [routerLink]="['/orders', o.id]" lines="2">
        <span matListItemTitle>{{ o.number }}</span>
        <span matListItemLine>{{ o.customer }} · {{ o.vehicle }}</span>
        <pdr-status-tag matListItemMeta [status]="o.status" display="text" />
      </a>
    }
  </mat-nav-list>
} @else {
  <table mat-table [dataSource]="orders()" matSort class="pdr-table">…</table>
}
```

## Overrides (`styles/components/md3/_data-grids.scss`)
```scss
@use '@angular/material' as mat;

// Template contract: <table mat-table class="pdr-table">, <th mat-header-cell class="pdr-th">,
// <tr mat-row class="pdr-row" [class.pdr-row--selected]>, <td mat-cell class="pdr-td">, <tr mat-footer-row class="pdr-footer-row">
.pdr-table {
  @include mat.table-overrides((
    background-color: transparent,
    header-headline-color: var(--mat-sys-on-surface),
    row-item-outline-color: var(--mat-sys-outline-variant),
  ));
  border-radius: 0; // never rounded, never outlined
}
.pdr-th { border-bottom: 2px solid var(--mat-sys-outline-variant); }      // header divider
.pdr-td { vertical-align: top; }                                          // first-line baseline
.pdr-table--no-row-dividers .pdr-td,
.pdr-row:last-child .pdr-td { border-bottom-color: transparent; }        // optional dividers, never on last row

// Hover / selection / links
@media (hover: hover) {
  .pdr-row:hover { background: var(--pdr-state-layer-on-surface-8); }
  .pdr-row:hover .pdr-cell-link { color: var(--mat-sys-primary); }
  .pdr-row:hover .pdr-cell-link:hover { text-decoration: underline; cursor: pointer; }
}
.pdr-row--selected { background: var(--mat-sys-primary-container); }
.pdr-cell-link { color: inherit; text-decoration: none; }

// Alignment
.pdr-col--end    { text-align: end; font-variant-numeric: tabular-nums; }
.pdr-col--center { text-align: center; }

// Footer
.pdr-footer-row .pdr-td { border-top: 1px solid var(--mat-sys-outline-variant); border-bottom-color: transparent; }
.pdr-footer--subtotal { font: var(--mat-sys-body-large); color: var(--mat-sys-on-surface-variant); }
.pdr-footer--total    { font: var(--mat-sys-title-medium); color: var(--mat-sys-on-surface); }
```
Row height / header styles = M3 table defaults.
