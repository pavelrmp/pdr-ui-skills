# Workflows

Figma page: **Workflows 🟢** `10826:965` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10826-965) · Figma Spec: [`11038:2962`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11038-2962)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Repair workflow horizontal`, `Repair workflow vertical`, `Service workflow horizontal`, `Worksteps`, `Worksteps vertical` · **Angular:** custom PDR components; `Wizard` maps to `<mat-stepper>` (to confirm) · **Sources:** components on this page; PDR Stepper and Status tags (Repair status) specs

> **No M3 component.** Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Workflows show where an order is in a defined process — the repair or service steps in the workshop — and guide people through multi-step tasks (wizard).

| Need | Use |
|---|---|
| Show the progress of a repair across workshop steps | `Repair workflow horizontal` / `vertical` |
| Show the progress of a service order | `Service workflow horizontal` |
| List the individual work steps of an order | `Worksteps` / `Worksteps vertical` |
| Guide people through a multi-step task (form) | **Wizard** (Stepper page) |
| Show one step’s status as a tag | `Repair status` (Status tags) |

## Figma components and properties

| Component | Properties |
|---|---|
| All other components | No properties |

## Decision rules

1. Horizontal workflows on wide screens; vertical workflows on narrow screens or in side panels. *(PDR proposal — confirm)*
2. **MUST** show exactly one current step; earlier steps completed, later steps upcoming (same rule as Stepper).
3. Workshop steps use the names and colours of `Repair status` (Status tags). *(PDR proposal — confirm)*
4. A workflow shows progress; to *do* a multi-step task use the **Wizard** (Stepper page).

## AI checklist

- [ ] Repair vs service workflow chosen by order type
- [ ] One current step
- [ ] Horizontal on wide screens, vertical on narrow ones
- [ ] Wizard / Stepper for multi-step tasks

## Open questions for the team

- **No properties:** the workflow components have no properties for the current step or states. Add a `Current step` / `Status` property so designs don’t need detaching.
- **Unused:** all components except `Repair workflow vertical` have no uses in this file.

---

# Part 2 — Angular implementation

### API

`pdr-wizard-steps` extends `CdkStepper` (keyboard, `linear`, step controls) — never a hand-rolled index.
```html
<pdr-wizard-steps [linear]="true" orientation="horizontal|vertical" variant="default|compact|application">
  <cdk-step [stepControl]="customerForm" label="Kunde">…</cdk-step>
</pdr-wizard-steps>
```
| Figma | Implementation |
|---|---|
| Wizard steps Status=Completed | check icon on `--mat-sys-primary` circle |
| Status=Current | `--mat-sys-primary` circle + title-small label, `aria-current="step"` |
| Status=Upcoming | outline circle `--mat-sys-outline`, label on-surface-variant |
| Service / Repair workflow horizontal / vertical | `<pdr-workflow [steps] orientation>` — read-only progress, uses `pdr-repair-status` per step |
| Worksteps (+vertical) | `<pdr-worksteps>` — checklist of `pdr-todo-button`s |

Standard multi-step forms without custom visuals → plain `mat-stepper` (`../md3/stepper.md`).
