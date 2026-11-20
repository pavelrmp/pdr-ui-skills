# Button toggle (Segmented buttons)

Figma page: **Button toggle (Segmented buttons) 🟢** `3330:91` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-91) · Figma Spec: [`10993:2158`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10993-2158)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Segmented button` (built from `Building Blocks/Segmented button/Button segment` start, middle and end), `Example/Segmented button` · **Angular:** `<mat-button-toggle-group>` / `<mat-button-toggle>` (multi-select: `multiple`) · **Sources:** [M3 Segmented buttons guidelines](https://m3.material.io/components/segmented-buttons/guidelines), [specs](https://m3.material.io/components/segmented-buttons/specs), [Button groups accessibility](https://m3.material.io/components/button-groups/accessibility)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

> **Note:** in M3 Expressive, segmented buttons are no longer recommended; the *connected button group* replaces them with mostly the same functionality. This library and Angular Material still use segmented buttons, so follow this spec.

## Purpose

Segmented buttons help people select options, switch views, or sort elements.

**Use when**

- Choosing **one** option, switching between views, or sorting, from 2–5 options → single-select.
- Selecting or sorting **several** options from 2–5 (e.g. filtering by price range) → multi-select.

**Don’t use when**

- There are more than 5 options → use chips or a select menu.
- The choice is a single on/off setting → use a switch.
- The action progresses the person to another step → use a button.

**Alternatives:** filter chips (a single selectable chip can replace a segmented button), radio buttons, single-select menus.

## Anatomy

| # | Element | Required | Notes |
|---|---|---|---|
| 1 | Container | Yes | Outlined, split into equal segments |
| 2 | Icon | No | Optional; a check icon marks the selected segment |
| 3 | Label text | Yes, unless icon-only | Centered |

## Figma components and properties

| Component | Property | Values |
|---|---|---|
| Segmented button | Segments | 2, 3, 4, 5, 6 |
| Button segment (start / middle / end) | Configuration | Label only, Label & icon, Icon only |
| Button segment | State | Enabled, Hovered, Focused, Pressed, Disabled |
| Button segment | Selected | True, False |
| Button segment | Label text · Icon | Text / icon swap |
| Example/Segmented button | Use case | Arrows, View (list-cards), Status filtering, Time range, Time range 2, View selection, Car view, Filtering |

Use the start segment first, middle segments in between, and the end segment last. Start from `Example/Segmented button` when the use case matches.

## Decision rules

1. **MUST** use 2–5 segments. **MUST NOT** use `Segments=6` — it exceeds the M3 maximum.
2. One option at a time (views, sorting, a single choice) → single-select: exactly one segment `Selected=True`.
3. Several options can apply (filters) → multi-select: any number of segments `Selected=True`.
4. (PDR) **SHOULD** keep the same Configuration in every segment of one control (all label, all icon, or all label & icon).
5. Use `Configuration=Icon only` only when every icon is unambiguous.
6. **MUST NOT** use a segmented button as an action (e.g. “Save”) — use a button.

## Behavior and interaction

- Selecting a segment in single-select deselects the previously selected one.
- In multi-select, each segment toggles independently.
- All segments share the container width equally.

## States

| State | When |
|---|---|
| Enabled | Default |
| Hovered | Pointer over a segment |
| Focused | Keyboard focus on a segment |
| Pressed | During click/tap |
| Disabled | Option unavailable |
| Selected = True / False | Combined with any state above |

## Content guidelines

- Keep labels short; each segment has the same width, so long labels truncate.
- Labels name the option, not an action.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use 2–5 related options | Use more than five segments |
| Use single-select for views and sorting | Mix label-only and icon-only segments in one control |
| Use multi-select for filters | Use a segmented button to trigger an action |

## Combining with other components

- **Page header (PDR):** MAY hold a segmented button to switch between views of the page.
- **Filters:** for more than 5 filter options, use filter chips or a dropdown instead.

## Accessibility

- **MUST** keep a 48 px target for each segment.
- Keyboard (connected button group guidance): **Tab** moves focus into the control, **arrow keys** move between segments, **Space** or **Enter** selects the focused segment.
- Label each segment; the container itself doesn’t need a label.

## Measurements

| Attribute | Value |
|---|---|
| Height | 40 px |
| Outline width | 1 px |
| Segment width | Container width ÷ number of segments |
| Left / right padding | Min 12 px |
| Space between icon and label | 8 px |
| Target size | 48 px |
| Label alignment | Center |

## AI checklist

- [ ] 2–5 segments (never 6)
- [ ] Single-select: exactly one selected · Multi-select: any number
- [ ] Same configuration in all segments
- [ ] Options, not actions
- [ ] 48 px targets

## Not covered by M3 (PDR conventions)

- **Selection-required behavior:** whether the last selected segment can be deselected isn’t defined in this library. Define it per use case.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Segmented button | `<mat-button-toggle-group [hideSingleSelectionIndicator]="false" aria-label="…">` |
| Segment | `<mat-button-toggle value="…">` (start/middle/end shapes are automatic) |
| Segments=N | N toggles |
| Selected=True | group `[(value)]` / `formControlName` |
| Configuration=Label & icon | `<mat-icon fontSet="material-symbols-outlined">` + text |
| Configuration=Icon only | icon + `aria-label` on the toggle |
| State=Disabled | `disabled` on toggle or group |
| Use case Filtering / Status filtering | `multiple` |

```html
<mat-button-toggle-group [(value)]="view" aria-label="Ansicht">
  <mat-button-toggle value="list"><mat-icon fontSet="material-symbols-outlined">list</mat-icon>Liste</mat-button-toggle>
  <mat-button-toggle value="cards">Karten</mat-button-toggle>
</mat-button-toggle-group>
```
Use case **Arrows** (prev/next) is not a toggle → two `matIconButton`s with `pdr-icon-btn--outlined`.

### Overrides


None — Figma matches M3 defaults. Do not add any.
