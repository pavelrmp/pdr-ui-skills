# Sliders

Figma page: **Sliders 🟢** `3617:2528` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3617-2528) · Figma Spec: [`11000:1666`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11000-1666)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Slider MD3` (Version v1–v4), `Slider 3`, `Slider right`, `Slider handle`, `Slider value handle`, `Slider MD2` (legacy) · **Angular:** `<mat-slider>` with `matSliderThumb` / `matSliderStartThumb` + `matSliderEndThumb` · **Sources:** [M3 Sliders guidelines](https://m3.material.io/components/sliders/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Sliders let people make selections from a range of values, such as volume or a price range.

| Variant | Use |
|---|---|
| Standard | Select **one** value from a range |
| Centered | Select a value from a range with positive and negative values |
| Range | Select **two** values that form a range |

| Configuration | Use |
|---|---|
| Continuous | Any value along the track |
| Discrete | Only specific values (stops) |

**Don’t use** (PDR) when an exact value must be typed → text field; when there are only a few named options → segmented button, radio buttons or a select menu.

## Anatomy

| # | Element | Notes |
|---|---|---|
| 1 | Active track | Part of the track up to the handle (range: between the two handles) |
| 2 | Inactive track | Remaining part |
| 3 | Handle | One (standard, centered) or two (range) |
| 4 | Value indicator | Optional; shows the current value while dragging |
| 5 | Stop indicators | Discrete stops and track ends |

## Figma components and properties

| Component | Notes |
|---|---|
| Slider MD3 | Version v1–v4 — M3 slider variants |
| Slider handle / Slider value handle | Building blocks: handle, handle with value indicator |
| Slider 3 / Slider right | PDR slider configurations |
| Slider MD2 | Legacy (Value: Default, less, more, planned, Done) — **don’t use for new work** |

## Decision rules

1. One value → standard slider. Values above and below zero → centered slider. A minimum and maximum → range slider (two handles).
2. Only specific values allowed → discrete (show stops); otherwise continuous.
3. The value indicator is optional; it isn’t required if the value is shown elsewhere (e.g. a field next to the slider).
4. Range sliders: show the value on **one handle at a time**.
5. **MUST NOT** use `Slider MD2` in new designs.

## Behavior and interaction

- Drag the handle or tap the track to change the value.
- Discrete sliders snap to stops.

## States

Handle: enabled, hovered, focused, pressed (dragging), disabled. These are built into the Figma versions; there’s no State property.

## Accessibility

- Keyboard:
  - **Tab** moves focus to the handle.
  - **Arrow keys** change the value by one step or stop.
  - **Space + arrow keys** change it by a larger interval.
- (PDR) Each handle needs an accessibility label; range sliders label the start and end handles.

## AI checklist

- [ ] Standard / centered / range chosen by the kind of value
- [ ] Discrete when only specific values are valid
- [ ] Value shown in the indicator or elsewhere
- [ ] Range sliders show one value at a time
- [ ] No Slider MD2

---

# Part 2 — Angular implementation

### Mapping


Range → `<input matSliderStartThumb>` + `<input matSliderEndThumb>`. *Slider MD2* (`10693:43630`) is legacy — don't implement new usages.

| Figma | Angular |
|---|---|
| Slider value handle | `discrete` (value label on drag) |
| Tick marks | `[showTickMarks]="true"` + `step` |
| Disabled | `disabled` on `mat-slider` |

### Overrides


None — Figma matches M3 defaults. Do not add any.
