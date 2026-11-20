# Toolbars (PDR)

Figma page: **Toolbars (PDR) 🟢** `3330:120` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-120) · Figma Spec: [`11038:3746`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11038-3746)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Order toolbar`, `Order toolbar compact`, `Order header toolbar`, `Filter calculation`, `Filter graphic calculation` · **Angular:** custom PDR components based on `<mat-toolbar>` (selectors to confirm) · **Sources:** components on this page; [M3 Toolbars](https://m3.material.io/components/toolbars/guidelines) (via the Toolbar MD3 spec)

> **No M3 component.** These are PDR toolbars for orders and calculations. They follow the M3 toolbar rules (see Toolbar spec). Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

| Component | Use |
|---|---|
| Order header toolbar | Actions at the top of an order page |
| Order toolbar · Order toolbar compact | Actions for an order inside panels or popovers; compact where space is limited |
| Filter calculation · Filter graphic calculation | Filter and view controls for calculation screens (table vs graphic view) |

## Decision rules

1. Follow the M3 toolbar rules: **at most one emphasised action**, overflow into a ⋮ menu, icon buttons of the same size with tooltips.
2. (PDR proposal — confirm) `Order toolbar compact` below ~600 px or inside popovers; `Order toolbar` otherwise.
3. Bulk actions for selected table rows go in a toolbar **above** the table (Data Grids rule).
4. Filters in calculation screens use filter chips and dropdown chips (Chips rules).

## AI checklist

- [ ] One emphasised action, overflow in ⋮
- [ ] Compact toolbar where space is limited
- [ ] Bulk actions above the table

## Open questions for the team

- **No properties:** none of the toolbars have properties (actions, compact vs full are separate components). Should `Order toolbar` get a `Size` property (Full, Compact) instead of two components?
- **Deprecated layers:** `Filter calculation` (10 layers), `Filter graphic calculation` (5), `Order header toolbar` (3) and `Order toolbar compact` (1) still contain `Deprecated/…` layers.
- **Unused:** none of these toolbars are used in this file. Are they current?

---

# Part 2 — Angular implementation


