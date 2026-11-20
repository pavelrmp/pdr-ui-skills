# Slide Toggle (Switch)

Figma page: **Slide Toggle 🟢** `3617:2527` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3617-2527) · Figma Spec: [`10999:1687`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10999-1687)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Switch`, `Form switcher` (PDR) · **Angular:** `<mat-slide-toggle>` · **Sources:** [M3 Switch guidelines](https://m3.material.io/components/switch/guidelines), [Checkbox guidelines](https://m3.material.io/components/checkbox/guidelines), [Button groups guidelines](https://m3.material.io/components/button-groups/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Switches turn a single setting on or off. They control **binary** options (one setting, on or off), not opposing ones.

**Use when** a standalone or more verbose option, such as a setting, is turned on or off.

**Don’t use when**

- Several related options can be selected from a list → checkboxes.
- Only one item can be selected from a list → radio buttons.
- Two **opposing** options (e.g. list vs. grid) → connected button group / segmented button.
- People expect a call to action → a button. **A switch can’t replace a button.**

## Anatomy

| # | Element | Required |
|---|---|---|
| 1 | Track | Yes |
| 2 | Handle | Yes |
| 3 | Icon in the handle | No (`Icon=Yes`) |
| 4 | Label | Yes, next to the switch |

## Figma components and properties

| Component | Property | Values |
|---|---|---|
| Switch | Checked | Yes, No |
| Switch | Icon | Yes, No |
| Switch | State | Enabled, Hovered, Focused, Pressed, Disabled |
| Form switcher | Position | Left, Right — PDR pattern |

## Decision rules

1. Single binary setting → `Switch`; a list of related options → checkboxes.
2. **MUST NOT** use a list of switches for options of one question — use checkboxes or radio buttons.
3. **MUST NOT** use a switch to trigger an action (e.g. “Send”) — use a button.
4. Opposing choices → segmented button, not a switch.
5. The change **SHOULD** take effect immediately; don’t require a separate Save for a single switch. *(PDR, in line with M3 guidance for on/off controls)*

## Behavior and interaction

Toggling moves the handle and changes `Checked`. (PDR) Selecting the label also toggles the switch.

## States

Enabled, Hovered, Focused, Pressed, Disabled — each with Checked Yes or No.

## Content guidelines

The label describes the setting in its on state, e.g. “Benachrichtigungen per E-Mail”. *(PDR)*

## Usage guidelines

| Do | Don’t |
|---|---|
| Use switches for standalone settings | Use switches for a list of related options |
| Label every switch | Use a switch as a call to action |
| Use a segmented button for opposing options | Use a switch for “List / Grid” |

## AI checklist

- [ ] Binary, standalone setting
- [ ] Labelled
- [ ] Not used as an action or for opposing options
- [ ] Lists of options use checkboxes or radio buttons

## Not covered by M3 sources used

- **`Form switcher`:** a PDR component (Position Left/Right). Its usage still needs to be documented.
- **Handle icons:** when to show them (`Icon=Yes`) isn’t covered by the sources used here.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Switch | `<mat-slide-toggle formControlName="x">Label</mat-slide-toggle>` |
| Checked=Yes | control value `true` |
| Icon=No | `hideIcon` |
| Icon=Yes | default |
| Form switcher Position=Left / Right | `labelPosition="after"` / `labelPosition="before"` |
| State=Disabled | `control.disable()` |

### Overrides


None — Figma matches M3 defaults. Do not add any.
