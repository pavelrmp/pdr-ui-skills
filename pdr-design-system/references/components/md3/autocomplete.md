# Autocomplete

Figma page: **Autocomplete 🟢** `10808:967` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10808-967) · Figma Spec: [`10993:2573`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10993-2573)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Autocomplete` (State Closed / Open), `Autocomplete panel` (Content Options / Grouped / No results) · **Angular:** `<mat-autocomplete>` attached to a `matInput` · **Sources:** [M3 Menus guidelines — Filtering](https://m3.material.io/components/menus/guidelines), [Text fields guidelines](https://m3.material.io/components/text-fields/guidelines), [Search accessibility](https://m3.material.io/components/search/accessibility)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

In M3, autocomplete is a **menu with a text field that filters its options**. As someone types, the list of menu options filters to show relevant results. This helps people find the right option quickly in a long list.

**Use when**

- People pick one (or several) values from a **long** list of known options, e.g. customers, vehicles, branches.

**Don’t use when**

- The list is short and fixed → use a select menu (Menus & Select).
- People search open-ended content and results, not a value for a field → use Search.
- There are only a few visible options → radio buttons, chips or segmented buttons.

## Anatomy

| # | Element | Required | Notes |
|---|---|---|---|
| 1 | Text field | Yes | Filled or outlined text field the menu is anchored to |
| 2 | Dropdown icon | No | Trailing arrow showing that the field has a nested selection |
| 3 | Clear icon | No | Appears only when input text is present |
| 4 | Menu | Yes | Temporary surface with the filtered options |
| 5 | Menu items | Yes | The options; MAY include supporting text |

## Figma components

| Component | Property | Values / use | Angular |
|---|---|---|---|
| Autocomplete | State | Closed (label, placeholder, dropdown arrow) · Open (focused field with typed text, clear icon, panel below) | `<input matInput [matAutocomplete]>` |
| Autocomplete panel | Content | Options (typed text in medium weight, first option active) · Grouped (group labels) · No results | `<mat-autocomplete>`, `<mat-option>`, `<mat-optgroup>` |

Built from `Text field` (Form fields) and `Menu list item 48` (Menu). Panel: surface-container, 4 px corners, elevation 2.

## Decision rules

1. **MUST** filter the menu options as the person types.
2. **MUST** open the menu when the person selects or types in the text field.
3. Single value → single-select menu: selecting an option fills the field and closes the menu.
4. Several values → multi-select menu: the menu stays open until dismissed.
5. **SHOULD** show the dropdown icon when the field offers a list of options.
6. **SHOULD** show the clear icon only when there is input text.
7. **MUST NOT** add buttons, switches or other direct actions inside menu items.

## Behavior and interaction

- Typing filters the options; items move smoothly into their new positions as the list filters.
- Selecting an option updates the field; single-select menus close, multi-select menus stay open.
- The menu is temporary and appears in front of all other UI.

## States

The text field and menu items use their own components’ states. Text field: enabled, hovered, focused, error, disabled. Menu item: enabled, hovered, focused, pressed, selected, disabled.

## Content guidelines

- The field label names what is being chosen (e.g. “Kunde”).
- Menu items show the option name; supporting text MAY add one distinguishing detail.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use for long lists of known values | Use for short lists — use a select menu |
| Filter as the person types | Put actions or switches inside menu items |
| Show a clear icon once text is entered | Use it as a general search for content |

## Accessibility

- **MUST** announce new or changed results to screen readers when suggestions appear.
- Menu item targets **MUST** be at least 48 × 48 px.
- The field’s accessibility label is the text field label.

## AI checklist

- [ ] Long list of known values → autocomplete; short list → select menu
- [ ] Menu filters while typing
- [ ] Single-select closes on selection, multi-select stays open
- [ ] No actions inside menu items
- [ ] Results are announced to screen readers

## Not covered yet

- **Loading state** while options load.
- **Multi-select with chips** in the field (`mat-chip-grid`).
- **Creating a new value** that isn’t in the list.

---

# Part 2 — Angular implementation

### Mapping

```html
<mat-form-field appearance="outline">
  <mat-label>Kunde</mat-label>
  <input matInput [formControl]="customer" [matAutocomplete]="auto" />
  <mat-autocomplete #auto [displayWith]="displayName" autoActiveFirstOption>
    @for (c of filtered(); track c.id) { <mat-option [value]="c">{{ c.name }}</mat-option> }
  </mat-autocomplete>
</mat-form-field>
```
Async results: debounce input (`300ms`), show `<mat-option disabled>` with `mat-progress-spinner diameter="20"` while loading.

### Overrides


None — Figma matches M3 defaults. Do not add any.
