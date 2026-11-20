# Toolbar

Figma page: **Toolbar 🟢** `10826:962` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10826-962) · Figma Spec: [`11007:2397`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11007-2397)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma component:** `Toolbar` · **Angular:** `<mat-toolbar>` · **Sources:** [M3 Toolbars guidelines](https://m3.material.io/components/toolbars/guidelines), [Icon buttons guidelines](https://m3.material.io/components/icon-buttons/guidelines), [Menus guidelines](https://m3.material.io/components/menus/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Toolbars display frequently used actions relevant to the current page.

| M3 type | Use |
|---|---|
| Docked toolbar | Spans the full width of the window; for **global** actions that stay the same across pages |
| Floating toolbar | Floats above the body content; for **contextual** actions relevant to the current page or content |

| Colour configuration | Use |
|---|---|
| Standard | Low emphasis; keeps attention on the body content |
| Vibrant | High emphasis; draws attention to the controls or signals a temporary mode (e.g. edit mode) |

(PDR) **Don’t use** a toolbar for top-level navigation → navigation bar, rail or drawer. Show the navigation bar on primary pages and a toolbar on subsequent pages with actions — **not both at the same time** at the bottom of the window.

## Anatomy

Container · icon buttons / buttons · optional emphasised action · optional overflow menu (⋮).

## Figma component and properties

`Toolbar` has no variant properties; adjust its nested icon buttons (Icon name, Style).

## Decision rules

1. Actions shared across pages → docked; page-specific actions → floating.
2. Emphasise **at most one** action (e.g. one Filled icon button). **MUST NOT** emphasise more than one action at a time.
3. Actions that don’t fit → move them into an overflow menu (⋮).
4. **MUST NOT** use multiple toolbars in compact windows.
5. Use icon buttons of the same size when actions have equal emphasis; icons **MUST** be unambiguous and have tooltips on web.
6. Bulk actions for selected table rows go in a toolbar **above** the table (PDR data-grid rule).

## Behavior and interaction

- Toolbar actions MAY open menus.
- Floating toolbars MAY act as tabs between related subsequent pages.

## States

None for the container; icon buttons use their own states.

## Usage guidelines

| Do | Don’t |
|---|---|
| Emphasise one key action | Emphasise several actions |
| Put overflow actions in a ⋮ menu | Show a toolbar and a navigation bar together at the bottom |
| Use a vibrant toolbar to signal a temporary mode | Use several toolbars on a phone |

## AI checklist

- [ ] Docked for global, floating for contextual actions
- [ ] Max one emphasised action
- [ ] Overflow in a menu
- [ ] Not combined with a navigation bar at the bottom
- [ ] Icon buttons with tooltips

## Not covered by M3 (PDR conventions)

- **Docked/floating and standard/vibrant:** not Figma properties yet.
- **Other toolbars:** PDR toolbars for orders and panels are on “Toolbars (PDR)”.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Toolbar | `<mat-toolbar class="pdr-toolbar">` with projected `matButton` / `matIconButton` / `mat-form-field` |
| Spacer between groups | `<span class="pdr-spacer"></span>` |

Domain toolbars (order, filters) → `../pdr/toolbars-pdr.md`.

### Overrides (`styles/components/md3/_toolbar.scss`)

```scss
@use '@angular/material' as mat;
.pdr-toolbar {
  @include mat.toolbar-overrides((
    container-background-color: var(--mat-sys-surface-container-lowest),
    standard-height: 88px,
  ));
  border-radius: var(--mat-sys-corner-large);
  padding: var(--pdr-space-16);
  gap: var(--pdr-space-8);
}
```
