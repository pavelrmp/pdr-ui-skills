# Menu

Figma page: **Menu 🟢** `10998:40437` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10998-40437) · Figma Spec: [`11009:1914`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11009-1914)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Dropdown menu`, `Menu list item 48`, `Menu list item 56`, `Menu items divider`, `Example/Dropdown menu` · **Angular:** `<mat-menu>` + `mat-menu-item`, opened with `[matMenuTriggerFor]` · **Sources:** [M3 Menus guidelines](https://m3.material.io/components/menus/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Menus display a list of choices on a temporary surface. They open from icon buttons, buttons, text fields, filter chips, or a right-click / press-and-hold.

| Use | Figma |
|---|---|
| Overflow menu (⋮) with extra actions | `Dropdown menu` from an Icon button |
| Context menu — actions for a selected item | `Dropdown menu` (`Example/Dropdown menu` · Contextual actions) |
| Filter menu from a filter chip | `Dropdown menu` (`Example/Dropdown menu` · Filter …) |
| Picking a value for a form field | Use **Select** instead |

**Don’t use a menu when** actions must be visible at all times → toolbar. A menu takes less space than radio buttons or chips; use those when options should stay visible.

## Anatomy

Menu item · leading icon (opt.) · menu item text · trailing icon (opt.) · badge (opt.) · trailing text (opt.) · container · supporting text (opt.) · label text (opt.) · gap (opt.) · divider (opt.)

## Figma components and properties

| Component | Properties |
|---|---|
| Dropdown menu | Show menu item 1–7 |
| Menu list item 48 | Type 1st, Checkboxes, Default · State Enabled, Hovered, Selected, Disabled (and Divider) · Show icon, arrow, supporting text |
| Menu list item 56 | Level 1st / 2nd · State Enabled, Hovered, Selected, Disabled · Left / Right icon · Show icon, arrow, supporting text |
| Menu items divider | — |
| Example/Dropdown menu | Use case: Filter employee, Filter created by, Filter Visibility, Contextual actions |

## Decision rules

1. Single-select menu: selecting an item replaces the previous selection and closes the menu.
2. Multi-select menu → `Menu list item 48`, `Type=Checkboxes`; the menu stays open until dismissed.
3. Group related items with a **gap** (max one or two per menu, never in scrollable menus) or a **divider**. On web, use a divider.
4. When an item can only be used under certain conditions, show it **disabled** rather than removing it.
5. **MUST NOT** put buttons, switches or other direct actions inside menu items.
6. The button that opened the menu keeps its look and shows a pressed state while the menu is open.
7. (PDR) Use `Menu list item 56` with `Level=2nd` for nested items; `Show arrow` marks items that open a submenu.

## Behavior and interaction

- Menus appear in front of all other UI.
- They close when an item is chosen (single-select) or when dismissed.
- Menu items MAY show keyboard commands as trailing text.

## States

Menu items: Enabled, Hovered, Selected, Disabled.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use a menu for extra or contextual actions | Hide always-needed actions in a menu — use a toolbar |
| Group items with one gap or a divider | Use many gaps or gaps in scrollable menus |
| Disable unavailable items | Remove items that are only temporarily unavailable |
| Keep menu item padding consistent | Add buttons or switches into menu items |

## Accessibility

Menu item targets **MUST** be at least 48 × 48 px.

## AI checklist

- [ ] Opened from a clear trigger (icon button, button, chip, right-click)
- [ ] Single-select closes; Checkboxes menu stays open
- [ ] No actions or switches inside items
- [ ] Max two gaps; divider on web
- [ ] Unavailable items disabled, not removed
- [ ] 48 px targets

## Not covered (PDR conventions)

- **`Menu list item 48` State=Divider:** a layout row, not an interaction state. To be moved to Type.

---

# Part 2 — Angular implementation

### Mapping
| Figma | Angular |
|---|---|
| Dropdown menu | `[matMenuTriggerFor]="menu"` + `<mat-menu #menu>` |
| Menu list item 48 Default | `<button mat-menu-item>` (+ `<mat-icon>` leading) |
| Type=Checkboxes | `<button mat-menu-item role="menuitemcheckbox" [attr.aria-checked]>` with `<mat-pseudo-checkbox [state]>`; keep menu open via `(click)="$event.stopPropagation()"` |
| State=Selected | `class="pdr-menu-item--selected"` + `aria-current="true"` |
| Divider / Menu items divider | `<mat-divider>` |
| Menu list item 56 Level 2nd | nested `[matMenuTriggerFor]` on a `mat-menu-item` |
| Dropdown menu clients | menu with `<pdr-avatar size="s">` leading |


### Overrides (`styles/components/md3/_menu.scss`)
```scss
.pdr-menu-item--selected { background: var(--mat-sys-secondary-container); color: var(--mat-sys-on-secondary-container); }
.pdr-menu--wide { min-width: 280px; } // via panelClass / class on mat-menu
```
