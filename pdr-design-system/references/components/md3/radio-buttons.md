# Radio buttons

Figma page: **Radio buttons 🟢** `3453:2024` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3453-2024) · Figma Spec: [`10999:1521`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10999-1521)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma component:** `Radio buttons` · **Angular:** `<mat-radio-group>` + `<mat-radio-button>` · **Sources:** [M3 Radio button guidelines](https://m3.material.io/components/radio-button/guidelines), [Switch guidelines — alternate selection controls](https://m3.material.io/components/switch/guidelines), [Lists guidelines](https://m3.material.io/components/lists/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Radio buttons let people select **one** option from a set. They’re the recommended way to allow a single selection.

| Need | Use |
|---|---|
| One option from a list | Radio buttons |
| Several related options | Checkboxes |
| A standalone on/off setting | Switch |
| One of 2–5 options shown as buttons, or switching views | Segmented button |
| Many options in little space | Select menu |

## Anatomy

| # | Element | Required |
|---|---|---|
| 1 | Radio button (selected / unselected) | Yes |
| 2 | Adjacent label | **Yes** |

## Figma component and properties

| Property | Values |
|---|---|
| Selected | True, False |
| State | Enabled, Hovered, Focused, Pressed, Disabled |

## Decision rules

1. **MUST** pair every radio button with an adjacent label that describes what it selects.
2. **MUST** allow exactly one selection per group — never more than one `Selected=True`.
3. **SHOULD** pre-select one option.
4. **SHOULD** list radio buttons vertically.
5. **MUST NOT** nest radio buttons or use them to select multiple options.
6. In single-select lists, use radio buttons — not checkboxes.

## Behavior and interaction

Selecting a radio button deselects the previously selected one in the same group.

## States

Enabled, Hovered, Focused, Pressed, Disabled — each with Selected True or False.

## Content guidelines

(PDR) Labels are short and describe the option. Options in a group are parallel and mutually exclusive.

## Usage guidelines

| Do | Don’t |
|---|---|
| Stack options vertically with one pre-selected | Allow two selected radio buttons |
| Label every radio button | Nest radio buttons |
| Use radio buttons for single-select lists | Use switches when only one item can be selected |

## AI checklist

- [ ] One selection only, one option pre-selected
- [ ] Every radio button has a label
- [ ] Vertical list, no nesting
- [ ] Checkboxes instead when several can be selected

## Not covered by M3 sources used

Keyboard interaction and accessibility labels aren’t listed in the sources used here. Follow Angular `mat-radio-group` defaults.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Group | `<mat-radio-group formControlName="x" aria-label="…">` |
| Radio | `<mat-radio-button value="a">Label</mat-radio-button>` |
| Selected=True | group value |
| State=Disabled | `disabled` on button or group |

Large tile-style choices → `../pdr/megaoptions-todo.md` (Megaoption).

### Overrides


None — Figma matches M3 defaults. Do not add any.
