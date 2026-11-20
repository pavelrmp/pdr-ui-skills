# Status tags

Figma page: **Status tags 🌕** `3346:263` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3346-263) · Figma Spec: [`11031:1765`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11031-1765)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🌕 In progress · **Figma components:** `Status`, `Process status`, `Employee status`, `Repair status`, `Appointment` · **Angular:** custom PDR components built on Angular Material tokens (selectors to confirm with development) · **Sources:** component properties and descriptions on this page; PDR Data Grids › Key principles; [M3 Color roles](https://m3.material.io/styles/color/roles), [M3 Chips](https://m3.material.io/components/chips/guidelines), [M3 Badges](https://m3.material.io/components/badges/guidelines)

> **No M3 component.** Status tags are a PDR pattern. Rules marked **(PDR proposal — confirm)** are suggestions derived from the components and need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Status tags show the state of a record — an order, an employee, a repair step, an appointment — as a short, colour-coded label that can be scanned at a glance, especially in tables and lists.

**Don’t use a status tag** to trigger an action → button or chip; to show a count or unread update on a navigation item → badge (M3); to filter content → filter chip (M3).

## Which component?

| Need | Component |
|---|---|
| A general state with a semantic tone (success, error, warning, info, neutral) | `Status` |
| The step of an order in the PDR process (e.g. “In Reparatur”, “Warte auf Teile”) | `Process status` |
| Availability of an employee (working, sick, on vacation …) | `Employee status` |
| A workshop step and its progress (Default / Planned / Done) | `Repair status` |
| The type of an appointment (Bringen, Holen, Besichtigung …) | `Appointment` |

## Figma components and properties

| Component | Properties |
|---|---|
| Status | Status: Success, Error, Warning, Info (label “In progress”), Neutral (label “Info”) · Size: Text, Icon + Text, Icon · Show arrow_drop_down · icon swaps per status |
| Process status | Status: 17 order steps (Kunde kontaktieren … Anlieferung) · Size: Text, Icon + Text, Icon · Show trailing icon |
| Employee status | Status: Working, Sick, On vacation, On break, Off duty, Not clocked in, Short-time work, Flextime, Training, Other · Size: Text, Icon + Text, Icon |
| Repair status | Step: 13 workshop steps · Status: Default, Planned, Done · Show text, Show leading icon, Show trailing icon |
| Appointment | Status: Besichtigung, Reparaturende, Reparaturstart, Bringen, Holen, Anlieferung, Auslieferung · Size · Show trailing icon |

## Decision rules

1. **MUST** use the domain component when one exists (Process, Employee, Repair, Appointment) instead of recreating it with `Status`.
2. **MUST NOT** recolour a status. Each value has a fixed colour (tables below); the colour is part of the meaning.
3. **MUST NOT** rely on colour alone: use `Size=Icon + Text` or `Size=Text`. Use `Size=Icon` only where the meaning is shown elsewhere (legend, tooltip). *(PDR rule — Data Grids)*
4. **Generic `Status` tones (as designed):**
   - `Success` → success container, label “Success” — completed / positive.
   - `Error` → error container — failed or blocking.
   - `Warning` → warning container — needs attention.
   - `Info` → info container, label **“In progress”** — work is ongoing.
   - `Neutral` → surface container, label **“Info”** — information without a state.
5. **`Repair status` shows progress per workshop step:** `Default` = not planned (surface container), `Planned` = scheduled (filled primary), `Done` = finished (filled success). The filled style (icons in `on primary` / `on success`) is intended for progress steps.
6. (PDR proposal — confirm) In dense tables use `Size=Text`; in cards and detail views `Size=Icon + Text`.
7. (PDR proposal — confirm) `Show arrow_drop_down` / trailing icon only when selecting the tag opens a menu to change the status; otherwise the tag is read-only.
8. Show **one** status tag per record and column; several states → several columns or a combined component (e.g. `Repair status` for steps).

### Process status — colour per step

| Colour | Steps |
|---|---|
| lime | Kunde kontaktieren · Termin vereinbaren · Fahrzeug kommt · Anlieferung · Warte auf Besichtigung |
| success | Schaden erfasst · Kalkulation |
| emerald | KV erstellen · Warte auf Freigabe |
| teal | Teilebestellung · Warte auf Teile |
| cyan | In Reparatur · Wartet auf Reparatur · Auslieferung |
| primary | Rechnung prüfen · Rechnungsstellung |
| indigo | Abgeschlossen |

### Employee status — colour per state

| Colour | States |
|---|---|
| success | Angestempelt (Working) |
| warning | Pause (On break) |
| error | Krank (Sick) · Feierabend (Off duty) · Nicht angestempelt (Not clocked in) |
| amber | Im Urlaub (On vacation) |
| lime | Kurzarbeit (Short-time work) |
| cyan | Gleitzeit (Flextime) |
| purple | Fortbildung (Training) |
| surface | Sonstiges (Other) |

### Appointment — colour per type

| Colour | Types |
|---|---|
| lime | Besichtigung · Anlieferung · Holen |
| indigo | Bringen |
| teal | Reparaturstart |
| cyan | Reparaturende |
| primary | Auslieferung |

## Behavior and interaction

- Status tags are read-only by default. A tag with a dropdown arrow opens a menu to change the status.

## Content guidelines

- Labels are short (one to three words) and name the state, not an action.
- **MUST** translate status values consistently: visible labels in the UI language (German), variant values in English — as in `Employee status` and `Repair status` (e.g. `Status=Sick` → “Krank”).

## Colour tokens

- **Container:** `<color> container` (e.g. `lime container`, `success container`).
- **Label text:** `on <color> container`.
- **Icon:** `<color>` (e.g. `lime`, `success`, `primary`) — the icon is one step stronger than the label.
- **Neutral / Sonstiges:** `on-surface-variant` for icon and label.

## Accessibility

- The label text carries the meaning; colour and icon support it.
- Interactive tags (with a dropdown arrow) need a 48 px target and a focus state.

## AI checklist

- [ ] Domain component used where it exists; Status only for generic states
- [ ] Icon + Text or Text — never colour alone
- [ ] Tone matches meaning (success / error / warning / info / neutral)
- [ ] Dropdown arrow only when the status can be changed
- [ ] One status per record and column

## Open questions for the team

- **Variant values still in German:** `Process status` and `Appointment` use German variant values (e.g. `Status=Kunde kontaktieren`), and one Process step is English (`Calculation`). Rename them to English to follow the language rule.
- **Angular:** what are the component selectors in code?

---

# Part 2 — Angular implementation

### Base: `pdr-status-tag`

24h, `corner-small`, padding 2/8 (`--pdr-space-2` / `--pdr-space-8`), gap 4, `--mat-sys-label-large`.
```html
<pdr-status-tag status="success" display="icon-text">Abgeschlossen</pdr-status-tag>
```
| Figma Size | `display` |
|---|---|
| Text | `"text"` |
| Icon + Text | `"icon-text"` |
| Icon | `"icon"` (requires `aria-label`) |

| Status | background | text/icon |
|---|---|---|
| success | `--pdr-sys-success-container` | `--pdr-sys-on-success-container` |
| error | `--mat-sys-error-container` | `--mat-sys-on-error-container` |
| warning | `--pdr-sys-warning-container` | `--pdr-sys-on-warning-container` |
| info | `--pdr-sys-info-container` | `--pdr-sys-on-info-container` |
| neutral | `--mat-sys-surface-container-high` | `--mat-sys-on-surface-variant` |
| extended (domain) | `--pdr-sys-{orange,amber,lime,emerald,teal,pink,purple,cyan,indigo}-container` | `--pdr-sys-on-…-container` |

### Domain tags (thin wrappers that map an enum → status/color + icon)

| Figma | Wrapper |
|---|---|
| Employee status | `<pdr-employee-status [status]="EmployeeStatus">` |
| Process status | `<pdr-process-status [status]="ProcessStatus">` |
| Appointment | `<pdr-appointment-tag [type]="AppointmentType">` |
| Delivery status | `<pdr-delivery-status [color] [flow]>` (interactive → `button` with state layer) |
| Check status | `<pdr-check-status [state]="'yellow'|'green'|'ai'">` |
| Repair status | `<pdr-repair-status [step] [status]="'default'|'planned'|'done'">` |
| Price chip | `<pdr-price-chip [amount] [updated]>` (State=Updated → `--pdr-sys-warning-container` highlight) |
| Premium feature | `<pdr-premium-badge>` (`--mat-sys-tertiary-container`) |

Keep each enum → color mapping in one `*.status-map.ts`; read exact color per Figma variant via MCP `get_variable_defs` before adding entries. Color must never be the only signal — always text or `aria-label`.
