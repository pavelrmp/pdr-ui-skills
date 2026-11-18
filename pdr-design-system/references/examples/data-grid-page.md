# Data grid page

Figma: **Example/Data grid** `10723:14870` · `Breakpoint` Desktop | Tablet | Mobile · `Content` Filled | Empty · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10723-14870)
Built on `app-shell.md` (app bar, page header, content container). Grid/breakpoints: `../foundations/grids-breakpoints.md`. Table rules: `../components/md3/data-grids.md` (Key principles are mandatory).

## Desktop / Tablet (frames 1440 / 1200)

```
App bar · Page header
Container (pad 0/24)
└── Panel (1128 max, surface-container-lowest, corner-large)
    ├── Panel title MD3 (56)
    ├── Filter row (48, pad 8/16, gap 8): Filtering chips · Dropdown chips · small text button "Filter zurücksetzen"
    ├── Table column (pad 0/16)
    │   ├── Header row 48 — 2 px outline-variant divider
    │   └── Rows 68 (2 lines) / 88 (3 lines), cell padding 12/8, top-aligned
    └── Paginator column (pad 24/16/16/16) — mat-paginator right-aligned
```
Column pattern from the example (tasks): ToDo checkbox 48 · Title (2 lines, key field) · Number 96 right-aligned · Avatar + text × 2 · Status tag · Date (2 lines) · Actions 40 (kebab).
A row with `--mat-sys-error-container` background marks an **overdue / critical** item — use sparingly and always with an icon or text cue too.

## Mobile (375)

```
App bar · Page header (mobile)
Panel (full width)
├── Panel title MD3 (64)
├── Filter container (48, horizontally scrollable chips)
└── List (mat-nav-list, rows 56 / 72 / 88)
FAB (primary, bottom-right, 16 px from edges) = page primary action
```

## Empty state (Content=Empty)
Keep app bar, header, panel and filter row; replace the table/list with `<pdr-empty-state type="no-data">` (or `no-results` when filters are active, with "Filter zurücksetzen"). Never render an empty table header.

## Angular skeleton
```html
<pdr-page-header title="Aufgaben" />
<div class="pdr-page-container">
  <pdr-panel>
    <pdr-panel-title>Offene Aufgaben</pdr-panel-title>
    <pdr-filter-bar [filters]="filters" (reset)="resetFilters()" />
    @if (loading()) { <pdr-skeleton-table-row [cols]="8" /> }
    @else if (!rows().length) { <pdr-empty-state [type]="hasFilters() ? 'no-results' : 'no-data'" /> }
    @else if (isHandset()) { <mat-nav-list>…</mat-nav-list> }
    @else { <table mat-table class="pdr-table" matSort [dataSource]="rows()">…</table> }
    @if (!isHandset()) { <mat-paginator class="pdr-paginator" [pageSizeOptions]="[10, 25, 50, 100]" /> }
  </pdr-panel>
</div>
@if (isHandset()) {
  <button matFab class="pdr-fab--primary pdr-fab--page" aria-label="Neue Aufgabe">
    <mat-icon fontSet="material-symbols-outlined">add</mat-icon>
  </button>
}
```
```scss
.pdr-fab--page { position: fixed; right: var(--pdr-space-16); bottom: calc(var(--pdr-space-16) + env(safe-area-inset-bottom)); }
.pdr-paginator { padding: var(--pdr-space-24) var(--pdr-space-16) var(--pdr-space-16); }
```
