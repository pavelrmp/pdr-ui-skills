# Megaoptions, ToDo

Figma page: **Megaoptions, ToDo** `10798:38006` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10798-38006)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Megaoption** `10849:1138` — `Selected` True|False · `State` Enabled|Hovered|Focused|Pressed|Disabled
- **To-do button** `4499:9686` — `Task` To do|Done · `State` Enabled|Hovered|Focused|Pressed|Disabled

## Megaoption
Large selectable tile (icon + title + description).
```html
<pdr-megaoption-group formControlName="type" aria-label="Auftragsart">
  <pdr-megaoption value="repair" icon="build" title="Reparatur" description="…" />
</pdr-megaoption-group>
```
Semantics = radio group (use `mat-radio-button` internally or `role="radiogroup"/"radio"` + roving tabindex; `[multiple]` → checkbox semantics). Selected: border `--mat-sys-primary` 2px + background `--mat-sys-primary-container`; Enabled: outline `--mat-sys-outline-variant`, `corner-medium`; Disabled: `--pdr-sys-on-surface-disabled`.

## To-do button
```html
<pdr-todo-button [done]="task.done" (doneChange)="toggle(task)">{{ task.title }}</pdr-todo-button>
```
`role="checkbox"` + `aria-checked`; Task=Done → check icon + `--pdr-sys-success` and strikethrough label. States via state layers (8/12%).
