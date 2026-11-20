# Sort Header

Figma page: **Sort Header 🟢** `10998:36773` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10998-36773) · Figma Spec: [`11009:3747`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11009-3747)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma component:** `Column header` · **Angular:** `matSort` on the table + `mat-sort-header` on each sortable column header · **Sources:** Angular Material Sort Header; PDR “Table (Data Grids) › Key principles · Table header”

> **M3 has no sort-header component.** All rules here are **PDR rules** from the table Key principles, aligned with Angular `matSort`.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

A sort header is a table column header that sorts the rows by that column when selected.

## Anatomy

| # | Element | Notes |
|---|---|---|
| 1 | Column title | label style, `on-surface-variant` |
| 2 | Sort indicator | Arrow showing ascending or descending order |
| 3 | Unsorted hint | `Show spinbox` — shows that the column can be sorted |

## Figma component and properties

| Property | Values | Meaning |
|---|---|---|
| Type | Col Left, Col center, Col right | Alignment, matching the cells below |
| State | Enabled | Not sorted |
| State | Hovered | Pointer over a sortable header |
| State | Pressed once | Sorted ascending |
| State | Pressed twice | Sorted descending |
| Show spinbox | True / False | Shows the sort hint on sortable columns |

## Decision rules

1. Align the header like its cells: text columns `Type=Col Left`, numeric columns `Type=Col right`, centred content `Type=Col center`.
2. Only sortable columns show the sort hint (`Show spinbox=True`); non-sortable columns show none.
3. **MUST** show exactly one sorted column at a time (`Pressed once` or `Pressed twice`); all other columns are `Enabled`.
4. Selecting a header cycles: ascending → descending → unsorted (Angular default).
5. (PDR proposal) Sort the key column (e.g. order number or date) by default when the table opens.
6. The header row uses a 2 px `outline-variant` divider and on-surface / on-surface-variant text (Table header rules).

## Behavior and interaction

- Click/tap on a sortable header changes the sort order and updates the arrow.
- Hover shows that the header is interactive.

## States

Enabled (unsorted), Hovered, Pressed once (ascending), Pressed twice (descending).

## Usage guidelines

| Do | Don’t |
|---|---|
| Align the header like the cells | Left-align the header of a numeric column |
| Show one sorted column | Show several columns as sorted |
| Show the hint only on sortable columns | Show sort arrows on columns that can’t be sorted |

## Accessibility

Sortable headers are interactive and **MUST** keep a 48 px target height and show focus. Announce the sort direction to screen readers (Angular `MatSortHeader` does this via `aria-sort`).

## AI checklist

- [ ] Header type matches the cell alignment
- [ ] Sort hint only on sortable columns
- [ ] Exactly one sorted column, with the correct direction
- [ ] 2 px header divider

## Not covered

- **Focused state:** not modelled in Figma yet.
- **State names:** `Pressed once` / `Pressed twice` could be renamed to `Sort=Ascending / Descending` for clarity.

---

# Part 2 — Angular implementation

### Mapping
| Figma | Angular |
|---|---|
| Column header (sortable) | `<th mat-header-cell *matHeaderCellDef mat-sort-header>` inside `<table mat-table matSort>` |
| Type=Col right | `class="pdr-th pdr-col--end"` + `arrowPosition="before"` (arrow stays next to the right-aligned title) |
| Type=Col center | `class="pdr-th pdr-col--center"` |
| Show spinbox=False | no `mat-sort-header` on that column (or `[disabled]="true"`) |
| State=Pressed once / twice | `matSortDirection="asc"` / `"desc"` on the active column |
| Default sort (PDR proposal) | `matSortActive="number" matSortDirection="desc"` on the table |

```html
<table mat-table class="pdr-table" [dataSource]="ds" matSort matSortActive="createdAt" matSortDirection="desc"
       (matSortChange)="announceSort($event)">
  <ng-container matColumnDef="amount">
    <th mat-header-cell *matHeaderCellDef mat-sort-header arrowPosition="before"
        class="pdr-th pdr-col--end" sortActionDescription="Nach Betrag sortieren">Betrag</th>
    <td mat-cell *matCellDef="let r" class="pdr-td pdr-col--end">{{ r.amount | currency:'EUR' }}</td>
  </ng-container>
</table>
```
```ts
announceSort(s: Sort) {
  inject(LiveAnnouncer).announce(s.direction ? `Sortiert ${s.direction === 'asc' ? 'aufsteigend' : 'absteigend'}` : 'Sortierung entfernt');
}
```
Header divider and text styles live in `data-grids.md` (Overrides).

### Overrides

None — Figma matches M3 defaults. Do not add any.
