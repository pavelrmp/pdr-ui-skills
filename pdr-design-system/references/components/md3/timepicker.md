# Timepicker

Figma page: **Timepicker 🟢** `10998:35675` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10998-35675) · Figma Spec: [`10998:35960`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10998-35960)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Dial picker`, `Keyboard picker` · **Angular:** `<mat-timepicker>` · **Sources:** [M3 Time pickers guidelines](https://m3.material.io/components/time-pickers/guidelines), [Dialogs](https://m3.material.io/components/dialogs/guidelines), [Text fields](https://m3.material.io/components/text-fields/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Date pickers let people select a date or a range of dates; dates can be past, present or future. Time pickers let people select a time.

**Don’t use a time picker** for nuanced or granular time selection, such as milliseconds.

## Variants

| M3 variant | Figma component | Use |
|---|---|---|
| Time picker — dial | `Dial picker` (Format 12/24 hour · Orientation Vertical/Horizontal) | Select hour and minute on a dial |
| Time picker — input | `Keyboard picker` (Format 12/24 hour) | Enter the time with the keyboard |

## Decision rules

1. Time selection → `Dial picker` by default; when the viewport is constrained → `Keyboard picker`. **MUST NOT** shrink (apply density to) the dial.
2. 12- or 24-hour format follows the system/user settings, not the picker. In 24-hour dials, hours 0–11 are on the outer ring and 12–23 on the inner ring.
3. Time pickers **MUST** change orientation (`Orientation`) or variant so they aren’t cropped by the screen edge.

## Accessibility

- All interactive targets **MUST** meet 48 × 48 px. Don’t increase density — it shrinks targets.
- Previous/next month and year buttons and the month/year dropdowns have the **button** role and a clear label.
- The accessibility label states the kind of input (e.g. “Event date”).
- Show keyboard shortcuts in tooltips so keyboard and screen-reader users can find them.

## AI checklist

- [ ] Docked on desktop next to a field; modal on mobile; input when the exact date is known
- [ ] Range variants for ranges
- [ ] Dial by default; keyboard picker when space is tight
- [ ] Never cropped at the screen edge
- [ ] Confirm with OK, dismiss with Cancel
- [ ] 48 px targets, no added density

---

# Part 2 — Angular implementation

### Mapping
| Figma | Angular |
|---|---|
| Keyboard picker | `<input matInput [matTimepicker]="tp">` + `<mat-timepicker-toggle matIconSuffix [for]="tp">` + `<mat-timepicker #tp>` |
| Dial picker | `<pdr-time-dial>` — no Angular Material equivalent (`mat-timepicker` is a dropdown list) |
| Format 12 / 24 hour | driven by locale (`MAT_DATE_LOCALE`, default `de-DE` → 24 h); never hard-code |
| Orientation Vertical / Horizontal | `pdr-time-dial` chooses by available height (landscape phones → horizontal) |

```html
<mat-form-field appearance="outline">
  <mat-label>Abholzeit</mat-label>
  <input matInput [matTimepicker]="tp" formControlName="pickupTime" />
  <mat-timepicker-toggle matIconSuffix [for]="tp" />
  <mat-timepicker #tp interval="15min" />
</mat-form-field>
```

### Overrides

None — Figma matches M3 defaults. Do not add any.
