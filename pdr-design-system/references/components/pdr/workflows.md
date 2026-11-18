# Workflows

Figma page: **Workflows** `10826:965` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10826-965)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Wizard steps** `8638:10996` — `Status` Completed|Current|Upcoming; **Wizard** `8638:11054`
- **Service workflow horizontal** `4912:2919`, **Repair workflow horizontal / vertical** `4856:22295`, `4856:22135`
- **Worksteps** `10735:46532`, **Worksteps vertical** `10735:46594`

## API
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

Standard multi-step forms without custom visuals → plain `mat-stepper` (`../md3/tabs-steppers.md`).
