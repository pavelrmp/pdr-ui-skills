# Select

Figma page: **Select 🟢** `3330:97` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-97) · Figma Spec: [`11009:2202`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11009-2202)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Dropdown` (select field), `Dropdown chip` · **Angular:** `<mat-select>` + `<mat-option>` inside `<mat-form-field>` · **Sources:** [M3 Menus guidelines](https://m3.material.io/components/menus/guidelines), [Text fields guidelines](https://m3.material.io/components/text-fields/guidelines), [Chips guidelines](https://m3.material.io/components/chips/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

A select is a field that opens a menu of options, so people can pick a value from a known list. M3 describes it as a **select menu** attached to a text field.

| Need | Use |
|---|---|
| One or several values for a form field from a short, known list | `Dropdown` (select field) |
| A filter value in a filter row | `Dropdown chip` (filter chip that opens a menu) |
| A long list people search | Autocomplete |
| A few options that should stay visible | Radio buttons, chips or segmented buttons |
| Actions instead of values | Menu |

## Anatomy

Label · selected value (or placeholder) · supporting text (opt.) · leading icon (opt.) · trailing **dropdown arrow** — it shows that the field has a nested selection · menu with options (see Menu).

## Figma components and properties

| Component | Properties |
|---|---|
| Dropdown | Style Standard/Filled, Outlined · State Enabled, Hovered, Focused, Error, Disabled · Label text · Value · Show label text, placeholder, supporting text, leading icon, trailing icon |
| Dropdown chip | Configuration · State (see Chips) |

The open menu uses the **Menu** components (`Dropdown menu`, `Menu list item 48 / 56`).

## Decision rules

1. **MUST** give every select a label.
2. One value → single-select: choosing an option fills the field and closes the menu.
3. Several values → multi-select: options with checkboxes (`Menu list item 48` · `Type=Checkboxes`); the menu stays open until dismissed.
4. Use the same field style as the other fields in the section (Filled or Outlined — see Form fields).
5. Errors: replace supporting text with error text (`State=Error`), as for text fields.
6. (PDR) Filter rows use `Dropdown chip`, not a select field.

## Behavior and interaction

- Selecting the field opens the menu; the field shows a pressed/focused state while open.
- Choosing an option updates the value; single-select closes the menu.

## States

Enabled, Hovered, Focused, Error, Disabled.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use a select for a known list of values | Use a select for actions — use a menu |
| Use autocomplete for long lists | Make people scroll a very long select menu |
| Match the style of the other fields | Mix filled and outlined fields in one section |

## Accessibility

Menu option targets **MUST** be at least 48 × 48 px. The label is the field’s accessible name.

## AI checklist

- [ ] Labelled select for known values; autocomplete for long lists
- [ ] Single-select closes, multi-select (checkboxes) stays open
- [ ] Same field style as the section
- [ ] Error text replaces supporting text
- [ ] Dropdown chip in filter rows

## Not covered

- **Field style names:** `Dropdown` uses “Standard/Filled” instead of “Filled”. Align with `Text field`.

---

# Part 2 — Angular implementation

### Mapping
| Figma Dropdown Style | Angular |
|---|---|
| Outlined | `<mat-form-field appearance="outline"><mat-select>` |
| Filled | `appearance="fill"` |
| Standard | `appearance="fill"` + `pdr-field--transparent` (see `form-fields.md`) |
| State=Error | validator + `<mat-error>` |

```html
<mat-form-field appearance="outline">
  <mat-label>Status</mat-label>
  <mat-select formControlName="status">
    @for (s of statuses; track s.id) { <mat-option [value]="s.id">{{ s.label }}</mat-option> }
  </mat-select>
</mat-form-field>
```


- Multi-select: `<mat-select multiple>` (options show checkboxes; panel stays open).
- Filter rows use `Dropdown chip` (`../md3/chips.md`), not `mat-select`.

### Overrides

None — Figma matches M3 defaults. Do not add any.
