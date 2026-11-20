# Skeleton loaders, empty and error states

Figma page: **Skeleton loaders, empty and error states 🟢** `10808:1015` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10808-1015) · Figma Spec: [`11038:2836`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11038-2836)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Skeleton`, `Skeleton list item`, `Skeleton card`, `Skeleton paragraph`, `Skeleton table row`, `Empty state illustration`, `Empty state/No data`, `Empty state/No results`, `Error state/Failed loading`, `Error state/No connection` · **Angular:** custom PDR components (selectors to confirm) · **Sources:** component descriptions on this page; M3 Progress indicators and Lists specs; PDR Brand loader and Data Grids rules

> **No M3 component.** Rules from the component descriptions are binding; others are marked **(PDR proposal — confirm)**.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

These components cover the moments when real content isn’t there: while it **loads** (skeleton), when there is **none yet** or **none matching** (empty state), and when it **can’t be loaded** (error state).

| Situation | Use |
|---|---|
| Content of a list, table, card or text is loading | **Skeleton** matching the content |
| Login, app start, logout | Brand loader (not skeleton) |
| A button, field or inline save is working | Circular progress (24) |
| An upload or measurable task | Linear progress (determinate) |
| No data yet | `Empty state/No data` |
| Search or filter returns nothing | `Empty state/No results` |
| Data failed to load | `Error state/Failed loading` |
| Device is offline | `Error state/No connection` |

## Figma components and properties

| Component | Properties / use |
|---|---|
| Skeleton | Shape: Text, Heading, Circle (avatar), Rectangle (image/media), Button, Chip · Effect: Static, Shimmer |
| Skeleton list item | Lines: 1, 2, 3 (match one-, two-, three-line list items) · Show avatar · Show trailing |
| Skeleton card | Media / content cards (order, customer, document) |
| Skeleton paragraph | Heading plus body lines, last line shorter |
| Skeleton table row | Data Grid rows — hide or duplicate cells to match the columns |
| Empty state illustration | Type: MFA, IP address, Email, Calculation, Notes, Pending, Customer, Vehicle … (96 × 96, monochrome) |
| Empty / Error states | Title · Description · Show description · Show action |

## Decision rules

**Skeletons**

1. **MUST** match the shape of the real content: list rows → `Skeleton list item` with the same Lines; tables → `Skeleton table row` with the same columns; cards → `Skeleton card`; text → `Skeleton paragraph`.
2. Use `Effect=Shimmer` for animated loading (the highlight moves left → right); `Static` for still mock-ups.
3. Show skeletons only inside the area that is loading; the rest of the screen stays usable. *(PDR proposal — confirm)*

**Empty states**

1. `Empty state/No data`: choose the illustration `Type` that matches the missing content, write what will appear here, and offer the action that creates it.
2. `Empty state/No results`: put the search term in the title and offer “Clear filters” as the action.
3. **MUST NOT** show an empty table header without rows — use an empty state instead (Data Grids › mobile rules).

**Error states**

1. `Error state/Failed loading`: the Retry action re-runs the request; keep the rest of the screen usable.
2. `Error state/No connection`: Retry re-checks the connection and reloads the content.

## Content guidelines (PDR proposal — confirm)

- Titles say what’s missing or wrong in a few words; descriptions say what to do.
- One clear action per state (e.g. “Kunde anlegen”, “Filter zurücksetzen”, “Erneut versuchen”).

## AI checklist

- [ ] Skeleton shape matches the real content
- [ ] Brand loader only for login / app start / logout
- [ ] Right state: no data · no results · failed loading · no connection
- [ ] Illustration type matches the content; one action
- [ ] No empty table headers

## Open questions for the team

- **Illustration types:** the set includes Error and No connection illustrations — are more types needed (e.g. Documents, Tasks)?

---

# Part 2 — Angular implementation

### API

```html
<pdr-skeleton shape="text|heading|circle|rectangle|button|chip" effect="shimmer" />
<pdr-skeleton-list-item [lines]="2" />  <pdr-skeleton-card />  <pdr-skeleton-paragraph />  <pdr-skeleton-table-row [cols]="6" />
<pdr-empty-state type="no-data|no-results" [illustration]="'customer'" (action)="create()" />
<pdr-error-state type="failed-loading|no-connection" (retry)="reload()" />
```

### Tokens

Skeleton fill `--mat-sys-surface-container-high`, shimmer highlight `--mat-sys-surface-container-low`; shapes use matching corner tokens (text `corner-extra-small`, button/chip `corner-full`/`corner-small`, circle `corner-full`). Shimmer disabled under `prefers-reduced-motion`.
Empty/error: illustration (SVG via MCP `download_assets`), title-large, body-medium on-surface-variant, primary action `matButton="filled"` / retry `matButton="outlined"`.

### A11y

Skeleton container `aria-busy="true"` + visually-hidden "Wird geladen"; individual skeletons `aria-hidden="true"`.
