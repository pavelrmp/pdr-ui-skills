# Table (Data Grids)

Figma page: **Table (Data Grids) 🟢** `3330:114` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-114) · Figma Spec: [`10995:4296`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10995-4296) · [`10950:17216`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10950-17216) · [`10955:1513`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10955-1513) · [`10955:1546`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10955-1546) · [`10955:1577`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10955-1577) · [`10955:1605`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10955-1605)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Column header`, `Cell one line`, `Cell 2+ lines`, `Cell input`, `Table footer` · **Angular:** `<table mat-table>` with `matSort` and `<mat-paginator>` · **Sources:** PDR “Data grid · Key principles” frames on this page; [M3 Density & targets](https://m3.material.io/foundations/layout/grids-spacing/density)

> **M3 has no data-table component.** All table rules here are **PDR rules** from the Key principles frames on this page. Only target size and density come from M3.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Data grids show many records with the same attributes so people can search, compare and select them.

**Use when** people compare or scan many records by several attributes (orders, invoices, employees).

**Don’t use when**

- There are only a few items or one attribute → use a list.
- The screen is compact (below 600 px) → use list items or cards (see “Tables on mobile devices”).

## Anatomy

| # | Element | Figma component |
|---|---|---|
| 1 | Header row | `Column header` (Col Left, Col right, Col center, Checkbox, date variants) |
| 2 | Rows of cells | `Cell one line` or `Cell 2+ lines` |
| 3 | Editable cell | `Cell input` |
| 4 | Footer | `Table footer` (Subtotal, Total) |
| 5 | Pagination | `Paginator` (Paginators page) |
| 6 | Bulk-action toolbar | Toolbar above the table, shown when rows are selected |

## Figma components and properties

| Component | Key properties |
|---|---|
| Column header | Type: Checkbox, Col Left, Col center, Col right, Col Day 1/2, Col Week, Col Range · Show spinbox (sort) |
| Cell one line | Type: Avatar+Name, Avatar+Text+Caption, Icon+Text, Status, Actions, Input, ProgressBar, Chart, GroupofAvatars … · Show edit/copy/pause/remove/more |
| Cell 2+ lines | Type: Order, Customer, Text, Text 2 Lines, Date 1/2, Status, Checkbox, Action, Avatar, ToDo, Dropdown … · Show underline (row divider) |
| Cell input | Filled: Default/Filled · State · Show status |
| Table footer | Type: Subtotal, Total |

## Decision rules (PDR)

**Content and columns**

1. Keep only the data needed to search, compare or select a row; everything else goes to the detail page.
2. Put the key field (e.g. order number) in the first column.
3. Place columns that are compared next to each other; combine related columns into one 2-line cell (e.g. vehicle + number plate).
4. Show data as icons, tags or statuses where possible; de-emphasise secondary data with `on-surface-variant`.

**Layout**

1. **MUST NOT** frame the table or round its corners. A table MAY sit in a rounded panel (`surface-container-lowest`, no border).
2. Header: separate it with a 2 px `outline-variant` divider. Use `on-surface` / `on-surface-variant` text, aligned like the cells below.
3. Text left-aligned; numbers right-aligned with monospaced digits — header included.
4. Align cell content to the first line of the row.
5. Avoid row dividers (`Show underline=false`) unless the table falls apart without them.

**Interaction**

1. Row hover: on-surface state layer 8 %.
2. Row selection: the checkbox selects the row and the row turns `primary-container`; show the count and bulk actions in a toolbar above the table.
3. Several independent clickable cells: plain text at rest, primary + underline on the hovered link only when the row is hovered.
4. Make the header sticky when it helps people keep their bearings while scrolling.

**Footer**

1. Use a footer only for totals, subtotals or pagination; label in the first column, total right-aligned under its column.
2. Emphasise the total (title/medium), not the subtotal; no colour for emphasis.
3. Pagination (`<mat-paginator>`) goes below the table; paginate from 50 rows.

**Mobile (< 600 px)**

1. Don’t shrink the table: turn rows into list items; key field first, 1–2 secondary values, status or amount trailing.
2. Use “Load more” instead of pages and a sticky summary bar for totals.

## States

Row: enabled, hovered (state layer 8 %), selected (`primary-container`). Cell input: Enabled, Hovered, Pressed. Loading: skeleton rows; no data: Empty state component.

## Accessibility

- Interactive elements in cells (checkboxes, icon buttons, links) **MUST** keep 48 × 48 px targets (M3).
- **MUST NOT** apply density by default; dense layouts are opt-in (M3).
- (PDR) Don’t rely on colour alone for status — use text or an icon with the chip.

## AI checklist

- [ ] Only necessary columns; key field first; related columns combined
- [ ] No table border or rounded corners; 2 px header divider
- [ ] Numbers and their header right-aligned
- [ ] No row dividers by default
- [ ] Hover 8 % state layer; selected rows primary-container + bulk toolbar
- [ ] Footer only for totals or pagination
- [ ] List items instead of a table below 600 px

## Not covered (to be defined)

- **Abbreviations in column headers:** the Key principles still say “TBD”.
- **Page-level secondary actions:** see the Page header component description.
- **Empty values:** decide on one convention (“—” or “offen”).
- **Row action menus:** when a row gets its own ⋮ menu versus opening on click.
- **Hiding a filtered column:** whether a column hidden because a filter covers it comes back when the filter is cleared.

---

# Part 2 — Angular implementation

### Mapping

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
| Col Week/Day/Range | planner grids → `../../examples/calendars.md` |
| Table footer Subtotal/Total | `*matFooterRowDef` + `<td mat-footer-cell>` (title-small) |

Rules: sticky header `*matHeaderRowDef="cols; sticky: true"`; row click → `(click)` on `tr` + `role="link"` + keyboard handler; empty/loading rows → `*matNoDataRow` with `<pdr-empty-state>` / `<pdr-skeleton-table-row>`.

### Key principles — detailed rules (Figma: "Data grid · Key principles", `10684:43362`, `10937:3494`, `10937:3504`, `10937:3514`, `10937:3524`)


Before laying out a table, analyse the content: what users search for, compare and select by, and how they move through rows and columns. These rules are mandatory for every `mat-table`.

#### Improving a table
1. **Keep only the data that matters.** Show only columns used to search, compare or select a row. Internal IDs, postcode, colour etc. go to the detail page.
2. **Order columns for comparison.** Values that are compared (Netto · MwSt. · Brutto) sit next to each other.
3. **Combine related columns.** Make + model + plate → one two-line cell (`pdr-cell-text` with caption) instead of three narrow columns.
4. **Key field first.** The identifying field (e.g. order number) is the first column and may be emphasised (`--mat-sys-title-small` / bold).
5. **Show data as icons, tags or statuses.** Replace yes/no or enum columns with `pdr-status-tag` / icons that can be scanned at a glance.
6. **De-emphasise secondary data** with `--mat-sys-on-surface-variant`, used sparingly — most text stays `--mat-sys-on-surface`. Never grey out everything.
7. **No outline, no rounded corners.** A table never has its own border or radius; it sits flush in its container. Structure comes from the header divider, alignment and spacing. It may sit inside a `pdr-panel` (`surface-container-lowest`, no border). Applies on desktop and mobile.

#### Header
- **Omit the header** for simple, self-explanatory tables (e.g. a short two-column list).
- **Align column titles like their cells** — numeric columns have right-aligned titles.
- **2 px divider** under the header in `--mat-sys-outline-variant`; no header background.
- **Header text** in `--mat-sys-on-surface`; secondary info (units) in `--mat-sys-on-surface-variant`. No blue or uppercase titles.
- **Select-all, sort and filter live in the header** (master checkbox, `mat-sort-header`, filter icon) — not as separate buttons above the table.
- **Abbreviations** in titles (SD, WS, INS, DG, GLM, GL, H+B, KV, MW, RW, REP…) always get a `matTooltip` with the full term.
- **Sticky header** (`*matHeaderRowDef="cols; sticky: true"`) when it helps users keep orientation and keeps sort/filter reachable.

#### Content
- **Row dividers are optional** (`--mat-sys-outline-variant`, 1 px) — only if the table falls apart without them. Never on the last row. Never a full cell grid.
- **Alignment:** text left; numbers right with tabular (monospaced) digits (`font-variant-numeric: tabular-nums`) and thousands grouping (`DecimalPipe` / `CurrencyPipe`, `de-DE`). Header of numeric columns right-aligned too.
- **Top-align cells to the first-line baseline** (`vertical-align: top`, consistent cell padding 12/8) — never vertically centre multi-line rows.
- **Row hover:** whole row gets an `on-surface` 8 % state layer (`--pdr-state-layer-on-surface-8`). One row at a time; never change text colour/weight. Pointer devices only (`@media (hover: hover)`).
- **Selected rows** (via checkbox) get `--mat-sys-primary-container`. Show the selection count and bulk actions in a toolbar above the table.
- **Clickable cells become links on row hover:** at rest they look like plain `on-surface` text; in the hovered row they turn `--mat-sys-primary`, and the cell under the pointer is underlined with `cursor: pointer`. Never make all clickable cells blue at rest.

#### Footer
- **Only when it adds information** (totals, subtotals, pagination).
- **Totals align with their column:** label ("Summe", "Zwischensumme") in the first column, left-aligned; values right-aligned with tabular digits.
- **Emphasise the total, not the subtotal:** Subtotal `--mat-sys-body-large` + `on-surface-variant`; Total `--mat-sys-title-medium` + `on-surface`. No colour highlighting.
- **1 px `outline-variant` divider above the footer**; same background as rows.
- **Pagination below the table**, right-aligned `<mat-paginator>` with 10 / 25 / 50 / 100. Paginate from 50 rows; infinite scroll only for feeds.
- **Sticky footer** (`*matFooterRowDef="cols; sticky: true"`) when the table scrolls inside its container. No actions in the footer — bulk actions belong in the toolbar above.

#### Mobile (< 600 px, `Breakpoints.Handset`)
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

### Overrides (`styles/components/md3/_data-grids.scss`)

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
