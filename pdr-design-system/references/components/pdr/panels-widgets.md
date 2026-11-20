# Panels & Widgets

Figma page: **Panels & Widgets 🟢** `3330:121` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-121) · Figma Spec: [`11037:9886`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11037-9886)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Panel`, `Panel title MD3`, `Panel title`, `Panel title interactive`, `Start page widget template` · **Angular:** custom PDR components (selectors to confirm) · **Sources:** components on this page; PDR Data Grids › Key principles (tables in panels); [M3 Cards](https://m3.material.io/components/cards/guidelines) for comparison

> **No M3 component.** Panels are the PDR content container. Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

A panel is the main content container of a page: a rounded surface (`surface container lowest`, 16 px corners) that groups one block of content — a table, a list, a form or a widget — under a panel title.

| Need | Use |
|---|---|
| A block of page content (table, list, form) | `Panel` + `Panel title MD3` |
| A widget on the start page / dashboard | `Start page widget template` |
| One item of a collection with its own actions (an order, a customer) | Card (M3 Cards) |

## Figma components and properties

| Component | Properties |
|---|---|
| Panel | Content Instance (swap) |
| Panel title MD3 | Show caption · Show search · Show add · Show more · Panel title · Underline text · Show leading icon · Number · Show number · Show info hint |
| Panel title | Show leading icon + Left Icon · Show trailing icon 1–3 · Show caption |
| Panel title interactive | Same as Panel title, interactive |
| Start page widget template | Content Instance (swap) |

## Decision rules

1. Page content sits in panels; a table **MUST NOT** have its own border — it sits flush inside the panel (Data Grids rule).
2. Use `Panel title MD3` for new panels: title, optional count (`Show number`), caption, and actions (search, add, ⋮ more). *(PDR proposal — confirm: MD3 version replaces `Panel title`)*
3. Panel actions: `Show search` for searching the panel content, `Show add` for creating an item, `Show more` (⋮) for the remaining actions.
4. Show the item count with `Show number` when the panel lists items (e.g. “In Reparatur 68”).
5. Dashboard widgets use `Start page widget template` so all widgets share size and padding. *(PDR proposal — confirm)*
6. Don’t nest panels in panels. *(PDR proposal — confirm)*

## AI checklist

- [ ] Content grouped in panels; tables flush, no border
- [ ] Panel title MD3 with count and actions
- [ ] Widgets from the template
- [ ] No panels inside panels

## Open questions for the team

- **Three panel titles:** `Panel title` (62 uses), `Panel title MD3` (43) and `Panel title interactive` (4). Which is current? Archive the others.
- **Property names:** `Show trailing icon 1 / 2 / 3` don’t say what each icon is for. Name them by function.
- **Deprecated layers:** `Panel title interactive` still contains `Deprecated/…` layers.

---

# Part 2 — Angular implementation

### API

```html
<pdr-panel>
  <pdr-panel-title [interactive]="true" (click)="expand()">Offene Aufgaben
    <button matIconButton pdrPanelAction aria-label="Mehr"><mat-icon fontSet="material-symbols-outlined">more_vert</mat-icon></button>
  </pdr-panel-title>
  …
</pdr-panel>
```
| Figma | Implementation |
|---|---|
| Panel | `:host { background: var(--mat-sys-surface-container-lowest); border-radius: var(--mat-sys-corner-large); padding: var(--pdr-space-16); }` |
| Panel title / MD3 | title-medium (MD3 variant: title-large) + actions slot |
| Panel title interactive | whole title is a `<button>` with state layer + chevron |
| Start page widget template | `<pdr-widget>` = `pdr-panel` with fixed header/footer slots in a CSS grid dashboard |
| Slider widgets mobile | horizontal scroll-snap container (`scroll-snap-type: x mandatory`) |
| Slider arrows Filled / Outlined / Ghost | `matIconButton` + `pdr-icon-btn--filled` / `--outlined` / default (see `../md3/buttons.md`) |
