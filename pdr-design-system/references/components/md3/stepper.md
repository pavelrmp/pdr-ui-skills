# Stepper (Wizard)

Figma page: **Stepper 🟢** `10998:36724` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10998-36724) · Figma Spec: [`11009:2485`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11009-2485)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Stepper`, `.Stepper element`, `Wizard`, `Wizard step` · **Angular:** `<mat-stepper>` (`orientation="horizontal" | "vertical"`, `linear`) with `<mat-step>` · **Sources:** Angular Material Stepper; PDR usage

> **M3 has no stepper component.** All rules in this spec are **PDR rules**, aligned with Angular `mat-stepper`.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

A stepper shows progress through a numbered sequence of steps, for example a multi-step form or the application flow.

**Use when** a task must be completed in a fixed order of steps.

**Don’t use when**

- Switching between related views of the same content → tabs.
- A single-step form → no stepper.
- Showing the status of an order over time → status tags or a timeline.

## Anatomy

| # | Element |
|---|---|
| 1 | Step element (number or check icon) |
| 2 | Step label |
| 3 | Connector line between steps |

## Figma components and properties

| Component | Property | Values |
|---|---|---|
| Stepper | Type | Default, compact, Application |
| .Stepper element | Status | Current, Upcoming, Completed |

## Decision rules

1. **MUST** show exactly one step `Status=Current`. Steps before it are `Completed`; steps after it are `Upcoming`.
2. `Type=Default` for forms with space for full labels; `Type=compact` where horizontal space is limited; `Type=Application` for the PDR application flow.
3. Use a linear stepper (people can’t skip ahead) when later steps depend on earlier ones; otherwise allow moving back to completed steps.
4. Keep the step count small and step labels short (one or two words).

## Behavior and interaction

- Completing a step marks it `Completed` and moves `Current` to the next step.
- Completed steps MAY be selected to go back and edit.

## States

Step status: Current, Upcoming, Completed. Error and disabled steps aren’t modelled in Figma.

## Wizard (Angular mat-stepper)

The **Wizard** is the full multi-step task: step headers, the content of the current step and the Back / Next actions. It mirrors Angular `<mat-stepper>`.

| Component | Properties | Angular |
|---|---|---|
| Wizard | Orientation: Horizontal, Vertical · Content (swap per step) · actions “Zurück” (Text) and “Weiter” (Filled) | `<mat-stepper orientation>`, `matStepperPrevious`, `matStepperNext` |
| Wizard step | Status: Upcoming, Current, Completed, Editable, Error · State: Enabled, Hovered, Focused · Step number · Label text · Show sublabel + Sublabel | `mat-step-header`, `matStepperOptional`, `[editable]`, `[hasError]` / `errorMessage` |

**Wizard rules**

1. Use the Wizard when people **do** a multi-step task (form); use `Stepper` / Workflows only to **show** progress.
2. Exactly one step `Status=Current`. Done steps are `Completed` (check) — or `Editable` (pencil) when people may go back and change them.
3. A step with invalid input shows `Status=Error` with the error message as sublabel.
4. Optional steps show `Show sublabel` with “Optional”.
5. Horizontal on wide screens; Vertical on narrow screens or in side sheets.
6. “Zurück” is a Text button, “Weiter” the only Filled button; on the last step the Filled button finishes the task (e.g. “Speichern”).

## Usage guidelines

| Do | Don’t |
|---|---|
| Use for ordered multi-step tasks | Use a stepper to switch views — use tabs |
| Show one current step | Mark several steps as current |
| Keep step labels short | Write sentences as step labels |

## AI checklist

- [ ] Ordered, multi-step task
- [ ] Exactly one Current step; Completed before, Upcoming after
- [ ] Type chosen by available space and flow
- [ ] Short step labels

## Not covered (to be defined)

- **Error state:** a step with invalid input has no Figma state yet. Angular supports error states.
- **Vertical layout:** Angular supports `orientation="vertical"`, but there’s no Figma variant for it.

---

# Part 2 — Angular implementation

### Mapping
| Figma Type | Angular |
|---|---|
| Default | `<mat-stepper [linear]="true" #s>` + `<mat-step [stepControl] label>`; buttons `matStepperNext` / `matStepperPrevious` |
| compact | `<pdr-wizard-steps variant="compact">` (see `../pdr/workflows.md`) |
| Application | `<pdr-wizard-steps variant="application">` |
| Vertical on mobile | `orientation="vertical"` via `BreakpointObserver` |


### Wizard mapping
| Figma Wizard step | Angular |
|---|---|
| Status=Current / Upcoming / Completed | managed by `mat-stepper` (`selectedIndex`, `[completed]`) |
| Status=Editable | `[editable]="true"` on `mat-step` (pencil icon) |
| Status=Error + sublabel | `[hasError]="ctrl.invalid && ctrl.touched"` + `errorMessage="…"` (needs `STEPPER_GLOBAL_OPTIONS` `{ showError: true }`) |
| Show sublabel “Optional” | `[optional]="true"` (label text via `MatStepperIntl.optionalLabel = 'Optional'`) |
| Orientation Horizontal / Vertical | `orientation` bound to `isHandset() ? 'vertical' : 'horizontal'` |
| Actions “Zurück” / “Weiter” | `<button matButton matStepperPrevious>Zurück</button>` · `<button matButton="filled" matStepperNext>Weiter</button>` |

### Overrides

None — Figma matches M3 defaults. Do not add any.
