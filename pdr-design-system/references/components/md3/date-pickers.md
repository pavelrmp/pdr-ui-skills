# Date pickers

Figma page: **Datepickers 🟢** `3330:122` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-122) · Figma Spec: [`10995:6855`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10995-6855)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Docked date picker`, `Modal date picker`, `Input date picker`, `Single date picker`, `Date range calendar`, `Day cell`, `Dial picker`, `Keyboard picker` · **Angular:** `<mat-datepicker>`, `<mat-date-range-picker>`, `<mat-timepicker>` · **Sources:** [M3 Date pickers guidelines](https://m3.material.io/components/date-pickers/guidelines), [Date pickers accessibility](https://m3.material.io/components/date-pickers/accessibility), [M3 Time pickers guidelines](https://m3.material.io/components/time-pickers/guidelines), [Dialogs](https://m3.material.io/components/dialogs/guidelines), [Text fields](https://m3.material.io/components/text-fields/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Date pickers let people select a date or a range of dates; dates can be past, present or future.

## Variants

| M3 variant | Figma component | Use |
|---|---|---|
| Docked date picker | `Docked date picker` (Type Day / Month / Year) | Appears just below the input field; ideal for dates in the near **and** distant past or future |
| Modal date picker | `Modal date picker` (Type Day / Year / Full-screen (range)) | Dialog; on compact screens (mobile) ranges use the full-screen variant |
| Modal date input | `Input date picker` (Type Single input / Range) | Manual entry with the keyboard; works well in compact layouts |

Building blocks: `Day cell` (Date, State Enabled/Hovered/Pressed), `Single date picker`, `Date range calendar`.

## Anatomy (date pickers)

Headline and supporting text · calendar grid of day cells · month/year navigation · edit icon to switch to keyboard input · actions (Cancel, OK, optional Clear).

Figma text properties: Headline, Supporting text, Headline (range), Supporting text (range). Toggle: Show clear button.

## Decision rules

1. Date picked from a text field on desktop/tablet → `Docked date picker`, opened from the field’s calendar icon.
2. Compact screens (mobile) → `Modal date picker`; for ranges, `Type=Full-screen (range)`.
3. The person knows the exact date (e.g. birth date) → `Input date picker` (keyboard entry). People **MAY** switch between the modal picker and modal input via the edit icon.
4. A range of dates → the range variants (`Range`, `Full-screen (range)`, `Date range calendar`).

## Behavior and interaction

- Modal date pickers and time pickers appear as modal windows above a scrim.
- A date is selected by tapping it and confirmed with **OK**; **Cancel** dismisses without changes.
- The calendar icon in a text field opens the date picker; the edit icon switches to keyboard input.

## States

`Day cell`: Enabled, Hovered, Pressed. Selected day, today and range highlight are shown in the pickers’ built-in examples.

## Content guidelines

- (PDR) The headline shows the selected date or range; supporting text describes what is being chosen (e.g. “Auslieferung wählen”).
- Action labels: Cancel and OK. (PDR) Show Clear only when the value may be empty.

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

## Not covered by M3 (PDR conventions)

- `Date range picker (Matero)` is a third-party pattern and now lives on the Calendars page; don’t use it for new work.
- Minimum/maximum dates and disabled days aren’t modelled in Figma yet.

---

# Part 2 — Angular implementation

### Mapping
| Figma | Angular |
|---|---|
| Docked date picker | `<input matInput [matDatepicker]="dp">` + `<mat-datepicker-toggle matIconSuffix [for]="dp">` + `<mat-datepicker #dp>` |
| Docked Type=Month/Year | `startView="multi-year"` / `"year"` |
| Modal date picker | same + `<mat-datepicker touchUi>` |
| Modal Full-screen (range) | `<mat-date-range-picker touchUi>` |
| Input date picker · Single input | `<input matInput [matDatepicker]>` typed by keyboard (the toggle stays optional) |
| Input date picker · Range | `<mat-date-range-input [rangePicker]="rp">` with `matStartDate` / `matEndDate` + `<mat-date-range-picker #rp>` |
| Show clear button | `<mat-datepicker-actions>` with Clear (`matButton`), Cancel (`matDatepickerCancel`), OK (`matDatepickerApply`) |

```html
<mat-form-field appearance="outline">
  <mat-label>Auslieferung</mat-label>
  <input matInput [matDatepicker]="dp" formControlName="delivery" />
  <mat-datepicker-toggle matIconSuffix [for]="dp" />
  <mat-datepicker #dp [touchUi]="isHandset()">
    <mat-datepicker-actions>
      <button matButton matDatepickerCancel>Abbrechen</button>
      <button matButton="filled" matDatepickerApply>OK</button>
    </mat-datepicker-actions>
  </mat-datepicker>
</mat-form-field>
```
Use `provideDateFnsAdapter()` (or the project adapter) with `MAT_DATE_LOCALE` `de-DE`; never format dates in templates manually. Min/max dates: `[min]`, `[max]`, `[matDatepickerFilter]`. Time selection: `timepicker.md`. Matero range picker: legacy, see `../pdr/pickers.md`.

### Overrides

None — Figma matches M3 defaults. Do not add any.
