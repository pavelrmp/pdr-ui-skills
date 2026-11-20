# Pickers

Figma page: **Pickers 🟢** `10850:42483` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10850-42483) · Figma Spec: [`11038:3888`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11038-3888)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Color sample`, `Palette 1`, `Palette 2`, `Touchspin`, `Date range picker (Matero)`; frame “Custom time picker” · **Angular:** custom PDR components; Matero date range picker is a third-party Angular component · **Sources:** components on this page; MD3 Datepickers / Timepicker specs

> **No M3 component.** M3 covers date and time pickers (see the Datepickers and Timepicker pages). Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

| Need | Use |
|---|---|
| Choose a colour | `Palette 1` / `Palette 2` built from `Color sample` |
| Increase or decrease a number step by step (e.g. quantity) | `Touchspin` |
| Pick a date, date range or time | **Datepickers** / **Timepicker** (MD3 pages) — not the Matero picker |

## Figma components and properties

| Component | Properties |
|---|---|
| Color sample | State: Enabled, Selected |
| Palette 1 · Palette 2 · Touchspin | No properties |
| Date range picker (Matero) | No properties — third-party, legacy |

## Decision rules

1. **MUST NOT** use `Date range picker (Matero)` for new work — use the M3 date range pickers (Datepickers page).
2. (PDR proposal — confirm) In a palette, exactly one `Color sample` is `State=Selected`.
3. (PDR proposal — confirm) Use `Touchspin` for small whole numbers with a clear minimum and maximum; use a text field for larger or free numbers.
4. (PDR proposal — confirm) Colour choices always show the colour name or a label as well (not colour alone), e.g. in a tooltip.

## AI checklist

- [ ] M3 Datepickers / Timepicker for dates and times
- [ ] One selected colour per palette
- [ ] Touchspin only for small step-wise numbers

## Open questions for the team

- **Palette 1 vs Palette 2:** what’s the difference? Can they become one component with a property?
- **Custom time picker:** the frame isn’t a component. Is it replaced by the MD3 Timepicker?
- **Matero picker:** archive it? It contains 5 `Deprecated/…` layers and has no uses in this file.
- **Touchspin:** no properties for states (disabled, min/max reached).

---

# Part 2 — Angular implementation

### Mapping

| Figma | Wrapper | Built from |
|---|---|---|
| Palette 1/2 + Color sample | `<pdr-color-picker formControlName [palette]>` | `role="radiogroup"`; each swatch `role="radio"` 32px `corner-full`; Selected → check icon + 2px `--mat-sys-on-surface` ring. Palette values = `ref.palette.*` tones from tokens.json |
| Touchspin | `<pdr-touchspin formControlName [min] [max] [step]>` | `matIconButton` (−/+) around `matInput type="number"` (outline); `ControlValueAccessor`; arrow keys step |
| Date range picker (Matero) | use `mat-date-range-input` + `mat-date-range-picker` with preset panel (`pdr-date-range-presets`, `matDateRangePickerActions`) | see `../md3/date-pickers.md` |
