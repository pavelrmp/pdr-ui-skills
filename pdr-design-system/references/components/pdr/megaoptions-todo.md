# Megaoptions, ToDo

Figma page: **Megaoptions, ToDo 🟢** `10798:38006` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10798-38006) · Figma Spec: [`11036:6842`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11036-6842)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Megaoption`, `To-do button` · **Angular:** Megaoption = `<mat-radio-group>` with one card per option (from the component description); To-do button = custom PDR component (selector to confirm) · **Sources:** component descriptions on this page; [M3 Radio button](https://m3.material.io/components/radio-button/guidelines), [M3 Checkbox](https://m3.material.io/components/checkbox/guidelines)

> **No M3 component.** Megaoption is a PDR radio card; To-do button is a PDR task control. Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Megaoption

### Purpose

A selectable radio card for choosing **one** option from a small set where each option needs a title, a short description and optionally a price (e.g. delivery options, service packages).

| Need | Use |
|---|---|
| One option, each needs title + description (+ price) | **Megaoption** |
| One option from a short list of simple labels | Radio buttons |
| Several options | Checkboxes |

### Figma component and properties

| Property | Values |
|---|---|
| Selected | True, False |
| State | Enabled, Hovered, Focused, Pressed, Disabled |
| Title · Description · Price | Text |
| Show description · Show price | Toggles |

### Decision rules

1. **MUST** use Megaoptions inside a radio group: **exactly one** card `Selected=True`.
2. **SHOULD** pre-select one option (as for radio buttons).
3. Show the price only when options differ in price; then show it on every card. *(PDR proposal — confirm)*
4. **MUST NOT** use more than ~5 Megaoptions in a group — use a radio list or a select instead. *(from the component description)*
5. The whole card is the click target; hover, focus and pressed show a state layer on the card. *(from the component description)*

## To-do button

### Purpose

The recommended way to let people mark a task as done.

### Figma component and properties

| Property | Values |
|---|---|
| Task | To do, Done |
| State | Enabled, Hovered, Focused, Pressed, Disabled |

### Decision rules

1. Use the To-do button for tasks people complete (e.g. in task lists and order to-dos) — not checkboxes. *(from the component description)*
2. `Task=To do` → open task; `Task=Done` → completed. Selecting the button toggles between them.
3. (PDR proposal — confirm) Keep the task label next to the button; the button alone has an accessible label like “Als erledigt markieren”.

## Accessibility

- Megaoption: the whole card is the target; keyboard follows radio-group behaviour.
- Both components need a visible focus state (`State=Focused`).

## AI checklist

- [ ] Megaoption only in a radio group, exactly one selected, one pre-selected
- [ ] Price on all cards or none
- [ ] To-do button for completing tasks, not a checkbox
- [ ] Focus state available

## Open questions for the team

- **To-do button selector:** what is the Angular component?

> Source — Megaoption description: “a selectable radio card for choosing one option from a small set … Use inside a radio group; only one card can be selected … Do not use for more than ~5 options.” To-do button description: “the recommended way to allow users to mark tasks as done.”

---

# Part 2 — Angular implementation

### Megaoption

Large selectable tile (icon + title + description).
```html
<pdr-megaoption-group formControlName="type" aria-label="Auftragsart">
  <pdr-megaoption value="repair" icon="build" title="Reparatur" description="…" />
</pdr-megaoption-group>
```
Semantics = radio group (use `mat-radio-button` internally or `role="radiogroup"/"radio"` + roving tabindex; `[multiple]` → checkbox semantics). Selected: border `--mat-sys-primary` 2px + background `--mat-sys-primary-container`; Enabled: outline `--mat-sys-outline-variant`, `corner-medium`; Disabled: `--pdr-sys-on-surface-disabled`.

### To-do button

```html
<pdr-todo-button [done]="task.done" (doneChange)="toggle(task)">{{ task.title }}</pdr-todo-button>
```
`role="checkbox"` + `aria-checked`; Task=Done → check icon + `--pdr-sys-success` and strikethrough label. States via state layers (8/12%).
