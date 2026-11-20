# Input (Text area)

Figma page: **Input 🟢** `10998:40057` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10998-40057) · Figma Spec: [`11009:3370`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11009-3370)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Text area` (with `Quick text input`, `AI input`, `Drag indicator`) · **Angular:** `<mat-form-field>` + `<textarea matInput>` (optional `cdkTextareaAutosize`) · **Sources:** [M3 Text fields guidelines](https://m3.material.io/components/text-fields/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

A text area is a multi-line text field for longer free text, such as notes, comments or descriptions. It follows all M3 text-field rules (see **Form fields**).

**Use when** people write more than one line of text.

**Don’t use when** the input is a single value (name, number, plate) → `Text field`; the value comes from a known list → Select or Autocomplete.

## Anatomy

| # | Element | Required |
|---|---|---|
| 1 | Container (filled) or outline (outlined) | Yes |
| 2 | Label text | Yes |
| 3 | Input text | Yes |
| 4 | Supporting text / error text | No |
| 5 | Drag indicator (resize) | No — PDR |
| 6 | Quick text input | No — PDR |
| 7 | AI input | No — PDR |

## Figma components and properties

| Property | Values |
|---|---|
| Style | Outlined, Filled |
| State | Enabled, Hovered, Focused, Error, Disabled, Read-only |
| Label text · Input text · Show input text | Text / toggle |
| Show placeholder · Placeholder text | Empty field: turn off Show input text, turn on the placeholder |
| Show required | Asterisk next to the label — explain it in supporting text |
| Show supporting text → Supporting text · Show counter · Counter | Exposed from the nested `Supporting text` (`<mat-hint>`, counter `<mat-hint align="end">`) |
| Show quick text input · Show AI input · Show drag indicator | Toggles (PDR features) |

## Decision rules

1. **MUST** give every text area a label.
2. Use the **same style** (Filled or Outlined) as the other fields in the section; filled has more emphasis than outlined.
3. Required: asterisk next to the label **and** an explanation.
4. Errors: replace supporting text with error text (`State=Error`). **MUST NOT** show both.
5. (PDR) `Show drag indicator` when people may need more space than the default height.
6. (PDR) `Show quick text input` for predefined text snippets; `Show AI input` only where an AI writing assistant is available for this field.

## Behavior and interaction

- Focusing shows the focused indicator; the label moves up.
- (PDR) The drag indicator resizes the text area vertically.

## States

Enabled, Hovered, Focused, Error, Disabled.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use for multi-line free text | Use for single values |
| Match the section’s field style | Mix filled and outlined in one section |
| Replace supporting text with error text | Show supporting and error text together |

## AI checklist

- [ ] Multi-line free text → text area
- [ ] Labelled; same style as the section
- [ ] Required: asterisk + explanation
- [ ] Error text replaces supporting text
- [ ] PDR add-ons only where they apply

## Not covered (PDR features to document)

- **`Quick text input` and `AI input`:** PDR components without M3 equivalents. Their exact behavior still needs to be documented.
- **Read-only:** shows pre-filled text people can’t edit, with an outline-variant border (PDR styling; M3 defines the behavior, not a style).

---

# Part 2 — Angular implementation

### Mapping
| Figma | Angular |
|---|---|
| Text area · Style Outlined / Filled | `<mat-form-field appearance="outline|fill">` + `<textarea matInput cdkTextareaAutosize cdkAutosizeMinRows="3">` |
| Show supporting text / counter | `<mat-hint>` / `<mat-hint align="end">{{ value.length }} / 500</mat-hint>` |
| Show required | `required` on the control + asterisk (Material adds it); explain in supporting text |
| State=Error | validator + `<mat-error>` (replaces the hint) |
| State=Read-only | `readonly` attribute + `class="pdr-field--readonly"` |
| Show drag indicator | `cdkTextareaAutosize` off + CSS `resize: vertical` on the textarea |
| Show quick text input | `<pdr-quick-text [for]="textarea">` — inserts predefined snippets (behaviour still to be documented) |
| Show AI input | `<pdr-ai-input [for]="textarea">` — only where an AI writing assistant exists for this field |

```html
<mat-form-field appearance="outline">
  <mat-label>Notiz</mat-label>
  <textarea matInput formControlName="note" cdkTextareaAutosize cdkAutosizeMinRows="3"></textarea>
  <mat-hint align="end">{{ form.value.note?.length ?? 0 }} / 500</mat-hint>
</mat-form-field>
```

### Overrides (`styles/components/md3/_input.scss`)
```scss
@use '@angular/material' as mat;
// Figma State=Read-only: outline-variant border (PDR styling)
.pdr-field--readonly { @include mat.form-field-overrides((outlined-outline-color: var(--mat-sys-outline-variant))); }
textarea.pdr-textarea--resizable { resize: vertical; }
```
