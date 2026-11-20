# Paginators

Figma page: **Paginators 🟢** `3617:2525` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3617-2525) · Figma Spec: [`10997:4375`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10997-4375)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma component:** `Paginator` · **Angular:** `<mat-paginator>` · **Sources:** PDR “Data grid · Key principles” (Table footer, Tables on mobile devices); [M3 Density & targets](https://m3.material.io/foundations/layout/grids-spacing/density)

> **M3 has no paginator component.** The rules below are **PDR rules** from the data-grid Key principles; target size comes from M3.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

A paginator splits a long table or list into pages and lets people move between pages and change the page size.

**Use when** a data grid on a desktop or tablet has more than about 50 rows.

**Don’t use when**

- The list is on a compact screen (below 600 px) → use a “Load more” button or infinite scroll with a progress indicator.
- The content is a feed → infinite scroll.

## Anatomy

| # | Element | Notes |
|---|---|---|
| 1 | Items per page | Dropdown with page-size options |
| 2 | Range label | e.g. “1–25 of 240” / “Page 1 of 20” |
| 3 | First / last page buttons | Optional |
| 4 | Previous / next page buttons | Required |

## Figma component and properties

| Property | Use |
|---|---|
| Show page size | Shows “Items per page” |
| Show multiple page size option | Shows the page-size dropdown with several options |
| Show first/last page | Shows first and last page buttons |

## Decision rules (PDR)

1. **MUST** place the paginator **below** the table, right-aligned. **MUST NOT** place it above the data.
2. Start paginating from 50 rows. Offer page sizes 10 / 25 / 50 / 100.
3. (PDR proposal — not yet in Key principles) Show first/last page buttons when there are many pages.
4. On compact screens, **MUST** replace the paginator with “Load more” or infinite scroll, and show totals in a sticky summary bar.
5. Totals belong in the table footer, not in the paginator.

## Behavior and interaction

- Previous/next move one page; first/last jump to the ends.
- Changing the page size returns to the first page and updates the range label. *(Angular default)*

## States

Navigation buttons: Enabled, Disabled (e.g. “previous” on the first page). Page-size field: Dropdown states.

## Accessibility

- Every button **MUST** have a 48 × 48 px target and an accessibility label (e.g. “Next page”).

## AI checklist

- [ ] Below the table, right-aligned
- [ ] Only from ~50 rows; page sizes 10/25/50/100
- [ ] Load more instead on mobile
- [ ] 48 px targets with labels

## Not covered

- Deprecated paginator components are on the Archive page. Don’t use them.

---

# Part 2 — Angular implementation

### Mapping

```html
<mat-paginator [length]="total" [pageSize]="25" [pageSizeOptions]="[10, 25, 50, 100]" showFirstLastButtons aria-label="Seiten" />
```
German labels: provide a `MatPaginatorIntl` subclass (`itemsPerPageLabel = 'Einträge pro Seite'`, `getRangeLabel` → "1–25 von 340").

### Overrides


None — Figma matches M3 defaults. Do not add any.
