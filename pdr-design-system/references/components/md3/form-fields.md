# Form fields (Text field, Code input)

Figma page: **Form fields 🟢** `3330:98` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-98) · Figma Spec: [`11009:2949`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11009-2949)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Text field`, `Code input` + `Code input cell` · **Angular:** `<mat-form-field>` (`appearance="fill" | "outline"`) + `matInput` · **Sources:** [M3 Text fields guidelines](https://m3.material.io/components/text-fields/guidelines), [Bidirectionality & RTL](https://m3.material.io/foundations/layout/bidirectionality-rtl), [Dialogs — error messages](https://m3.material.io/components/dialogs/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Text fields let people enter text into a UI, typically in forms and dialogs.

| Need | Use |
|---|---|
| A single line of text | `Text field` |
| Several lines (notes, comments) | `Text area` — see **Input** |
| A one-time code | `Code input` |
| Searching content | Search components (M3 Search) |
| Choosing from known values | Select field or autocomplete (Menus & Select, Autocomplete) |

## Anatomy

| # | Element | Required |
|---|---|---|
| 1 | Container (filled) or outline (outlined) | Yes |
| 2 | Label text | Yes |
| 3 | Input text / placeholder | Yes |
| 4 | Leading icon | No |
| 5 | Trailing icon (clear, dropdown, error, valid) | No |
| 6 | Supporting text / error text | No |
| 7 | Character counter | No |

## Figma components and properties

| Component | Properties |
|---|---|
| Text field | Label text · Input text · Placeholder text · Show supporting text · Show leading icon / Leading Icon Instance · Show trailing icon / Trailing Icon instance · Style · State |
| Code input | State Enabled, Error, Disabled |
| Code input cell | State Enabled, Hovered, Focused, Filled, Error, Disabled |

## Decision rules

1. **Filled vs outlined:** filled text fields have **more** visual emphasis than outlined ones. Choose one style per section; use outlined in one section and filled in another only to separate sections.
2. **MUST** give every field a label.
3. **Required fields:** show an asterisk (\*) next to the label **and** explain it — either in supporting text, or by noting that asterisks mark required fields.
4. **Errors:** for fields that validate their content, **replace** supporting text with error text and show the trailing error icon. **MUST NOT** show error text *in addition to* supporting text — it shifts the content.
5. Show errors **inline** at the field. General errors (e.g. network) go in a basic dialog. Show all errors at once.
6. **Read-only** fields show pre-filled text that people can’t edit.
7. Icons are optional. Leading and trailing icons swap sides in RTL.
8. A trailing **dropdown icon** signals a nested selection; a **clear icon** appears only when there is input text.

## Behavior and interaction

- Focusing the field moves the label up and shows the focused indicator.
- In error state, the error text and icon replace the supporting text until the input is valid.

## States

Enabled, Hovered, Focused, Error, Disabled (Code input cell). Text field states are set through its Style and State variants. Read-only is a configuration, not a separate Figma state.

## Content guidelines

- (PDR) Labels name the information requested (e.g. “Kennzeichen”).
- Supporting text gives a hint or format; error text explains briefly what is wrong and how to fix it.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use one field style per section | Mix filled and outlined fields randomly |
| Replace supporting text with error text | Show supporting and error text together |
| Mark and explain required fields | Use an asterisk without explanation |
| Show errors inline at the field | Collect field errors only in a dialog |

## Accessibility

- (PDR) The label is the field’s accessibility name — never rely on placeholder text alone.
- Errors use error text and a trailing error icon, not only colour.

## AI checklist

- [ ] Every field has a label
- [ ] One style (filled or outlined) per section
- [ ] Required fields: asterisk + explanation
- [ ] Error text replaces supporting text; error icon shown
- [ ] Clear icon only with input; dropdown icon only for nested selection

## Not covered by M3 (PDR conventions)

- **`Code input`:** a PDR pattern.

---

# Part 2 — Angular implementation

### Mapping — Text field

| Figma | Angular |
|---|---|
| Style=Outlined | `<mat-form-field appearance="outline">` |
| Style=Filled | `<mat-form-field appearance="fill">` |
| Style=Transparent BG | `appearance="fill"` + `class="pdr-field--transparent"` |
| State=Error | validator + `<mat-error>`; never force with CSS |
| State=Disabled | `control.disable()` (not the `disabled` attribute with reactive forms) |
| Supporting text | `<mat-hint>` (`align="end"` for counters) |
| Leading / trailing icon | `<mat-icon matPrefix>` / `<mat-icon matSuffix>`; clear button = `<button matIconButton matSuffix>` |

```html
<mat-form-field appearance="outline">
  <mat-label>Kennzeichen</mat-label>
  <input matInput formControlName="plate" />
  <mat-hint>z. B. B-AB 1234</mat-hint>
  @if (form.controls.plate.hasError('required')) { <mat-error>Pflichtfeld</mat-error> }
</mat-form-field>
```

### Code input

`<pdr-code-input [length]="6" formControlName="otp">`. Implements `ControlValueAccessor`; each cell reuses outline field tokens (`outline`, `corner-extra-small`), states Enabled|Focused|Filled|Error|Disabled. Use `autocomplete="one-time-code"` and `inputmode="numeric"`.

### Overrides (`styles/components/md3/_form-fields.scss`)

```scss
@use '@angular/material' as mat;
// Figma Style=Transparent BG (also Dropdown Style=Standard)
.pdr-field--transparent { @include mat.form-field-overrides((filled-container-color: transparent)); }
```
Heights, outline color and radius = M3 defaults.
