# Checkboxes

Figma page: **Checkboxes 🟢** `3617:2526` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3617-2526) · Figma Spec: [`10995:1981`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10995-1981)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Checkbox`, `Checkbox with label` · **Angular:** `<mat-checkbox>` · **Sources:** [M3 Checkbox guidelines](https://m3.material.io/components/checkbox/guidelines), [Checkbox accessibility](https://m3.material.io/components/checkbox/accessibility), [Switch guidelines](https://m3.material.io/components/switch/guidelines), [Lists guidelines](https://m3.material.io/components/lists/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Checkboxes let people select one or more options from a list, or turn an item on or off. A parent checkbox allows easy selection or deselection of all items.

**Use when**

- Several related options can be selected from a list.
- Rows in a table or list can be selected for bulk actions.

**Don’t use when**

- Only one option can be selected → radio buttons.
- A standalone setting turns on or off immediately → switch.
- A list consists of multiple options → **don’t** use switches; use checkboxes (they imply related items and take less space).

## Anatomy

| # | Element | Required |
|---|---|---|
| 1 | Container (box) | Yes |
| 2 | Icon (check or dash) | When selected or indeterminate |
| 3 | Label text | Yes, except in table rows/headers where the column or row provides context |

## Figma components and properties

| Component | Property | Values |
|---|---|---|
| Checkbox | Select | Unselected, Selected, Indetermined |
| Checkbox | State | Enabled, Hovered, Focused, Pressed, Disabled |
| Checkbox with label | Show label · Label text | Toggle / text |

## Decision rules

1. Use `Checkbox with label` for options in forms and lists. Use `Checkbox` alone only where the context labels it (table rows, table header “select all”).
2. Parent–child groups:
   - All children selected → parent `Select=Selected`.
   - No children selected → parent `Select=Unselected`.
   - Some, but not all, children selected → parent `Select=Indetermined`.
3. Selecting an indeterminate parent **MUST** select all its children; checking a parent checks all children; unchecking it unchecks all children.
4. Each checkbox can be selected or unselected independently of the others in its group.
5. If a checkbox turns something on or off, the action **SHOULD** take effect immediately.

## Behavior and interaction

- Selecting either the checkbox or its label toggles the option.
- The selected state is shown clearly and instantly.

## States

| State | When |
|---|---|
| Enabled | Default |
| Hovered | Pointer over the checkbox or label |
| Focused | Keyboard focus |
| Pressed | During click/tap |
| Disabled | Option unavailable |
| Selected / Unselected / Indeterminate | Combined with any state above |

## Content guidelines

- The label describes the option being selected.
- (PDR) In parent–child groups, the parent label describes the whole group (e.g. “Alle auswählen”).

## Usage guidelines

| Do | Don’t |
|---|---|
| Use checkboxes for multiple related options | Use switches for a list of options |
| Use a parent checkbox to select many items at once | Use checkboxes when only one option may be chosen |
| Make the label clickable | Leave a checkbox unlabeled outside a table context |

## Combining with other components

- **Lists:** multi-select lists pair well with checkboxes; single-select lists use radio buttons, not checkboxes.
- **Data grids (PDR):** the header checkbox selects all rows; selected rows turn `primary-container` and show a bulk-action toolbar (see Data Grids › Key principles).
- **Tree:** use Indetermined on parents with partial selection.

## Accessibility

- The accessibility label is typically the same as the adjacent text label; screen readers read the label followed by the role.
- The UI text **MUST** be linked to the checkbox.

## AI checklist

- [ ] Multiple related options → checkboxes; single choice → radio buttons
- [ ] Parent shows Indetermined when only some children are selected
- [ ] Label provided, except where table context labels it
- [ ] Label and box are both clickable

## Not covered by M3 sources used (to verify)

- **Error state:** M3’s checkbox specs define one, but the Figma component has no Error state yet.
- **Keyboard shortcuts:** not listed in the sources used here.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Select=Selected / Unselected | `[checked]` or `formControlName` |
| Select=Indetermined | `[indeterminate]="true"` (e.g. "select all" with partial selection) |
| State=Disabled | `control.disable()` / `[disabled]` |
| Checkbox with label | `<mat-checkbox>Label</mat-checkbox>`; label before → `labelPosition="before"` |
| Table row selection | see `data-grids.md` (`SelectionModel`) |

### Overrides


None — Figma matches M3 defaults. Do not add any.
