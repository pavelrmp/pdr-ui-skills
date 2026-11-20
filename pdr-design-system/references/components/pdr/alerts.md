# Alerts

Figma page: **Alerts 🟢** `3330:109` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-109) · Figma Spec: [`11032:4695`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11032-4695)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Alert filled`, `Register device card` (recovered example) · **Angular:** custom PDR component built on Angular Material tokens (selector to confirm) · **Sources:** component properties and descriptions on this page; [M3 Snackbar](https://m3.material.io/components/snackbar/guidelines) and [M3 Dialogs](https://m3.material.io/components/dialogs/guidelines) for the neighbouring patterns

> **No M3 component.** M3 has no inline alert. Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

An alert is a persistent, inline message inside a page or panel that tells people about a state that matters for the current content — e.g. a missing registration, an approaching deadline or a successful setup.

| Need | Use |
|---|---|
| Message that stays visible in the page until the situation changes | **Alert** |
| Brief feedback about a process, disappears on its own | Snackbar (M3) |
| Blocking decision or critical information | Dialog (M3) |

## Anatomy

| # | Element | Figma |
|---|---|---|
| 1 | Container in the message colour | `Message` |
| 2 | Icon | `Show icon` |
| 3 | Title | `Show title` |
| 4 | Description | Always shown |
| 5 | Actions (text buttons) | `Show actions` |

## Figma component and properties

| Property | Values |
|---|---|
| Message | Info, Success, Warning, Error |
| Style | Standard (action on the right, one row, 68 px), Longer action (actions below the text, 116 px) |
| Show title · Show icon · Show actions | Toggles |

## Decision rules

1. Choose `Message` by meaning: **Info** = neutral information · **Success** = something worked · **Warning** = needs attention soon · **Error** = something failed and needs action. *(PDR proposal — confirm)*
2. Short action label that fits next to the text → `Style=Standard`; long label or two actions → `Style=Longer action`.
3. **SHOULD** keep `Show icon` on — the icon carries the meaning together with the colour (never colour alone).
4. (PDR proposal — confirm) Show at most one alert per section; place it at the top of the content it refers to.
5. (PDR proposal — confirm) Actions are text buttons that solve the situation (e.g. “Gerät registrieren”); a close action only when the alert can be dismissed.
6. Transient feedback → use a snackbar instead; blocking decisions → a dialog.

## Content guidelines

- Title: the situation in a few words. Description: what it means and what to do.
- Action labels name the result, in sentence case.

## AI checklist

- [ ] Persistent, inline information → alert (not snackbar or dialog)
- [ ] Message type matches meaning
- [ ] Icon shown
- [ ] Standard for short actions, Longer action for long or two actions

## Open questions for the team

- **Buttons:** the actions inside `Alert filled` still use `Deprecated/Button`. Swap them to the current Button (Text) component.
- **`Register device card`:** a recovered product example (push-notification registration) with a default “Main action” property. Keep it as an example or move it to the Examples page?
- **Dismissible alerts:** is there a close (×) variant?

---

# Part 2 — Angular implementation

### API

```html
<pdr-alert type="warning" layout="inline" [dismissible]="true">
  <span pdrAlertTitle>Prüfung ausstehend</span>
  Bitte Rechnung prüfen.
  <button matButton pdrAlertAction>Prüfen</button>
</pdr-alert>
```
| Figma | Input |
|---|---|
| Message=Warning/Info/Success/Error | `type="warning|info|success|error"` |
| Style=Standard | `layout="inline"` (action right) |
| Style=Longer action | `layout="stacked"` (action below text) |

### Tokens

| type | background | text / icon | icon |
|---|---|---|---|
| warning | `--pdr-sys-warning-container` | `--pdr-sys-on-warning-container` | `warning` |
| info | `--pdr-sys-info-container` | `--pdr-sys-on-info-container` | `info` |
| success | `--pdr-sys-success-container` | `--pdr-sys-on-success-container` | `check_circle` |
| error | `--mat-sys-error-container` | `--mat-sys-on-error-container` | `error` |

Radius `--mat-sys-corner-extra-small`, padding 12/16, gap 12, title `--mat-sys-title-medium`, body `--mat-sys-body-medium`.

### A11y

`role="alert"` for error/warning raised by user action, `role="status"` otherwise. Dismiss button: `matIconButton` with `aria-label="Schließen"`.

### Register device card

`<pdr-register-device-card [registered]>` — `mat-card appearance="outlined"` + filled `matButton` (CTA) or success `pdr-status-tag` (Registered).
