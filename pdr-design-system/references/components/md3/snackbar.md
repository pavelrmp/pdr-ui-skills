# Snackbar

Figma page: **Snackbar 🟢** `10745:46606` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10745-46606) · Figma Spec: [`10999:1858`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10999-1858)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Snackbar` (building blocks: `.Building Blocks/Snackbar action`, `.Building Blocks/Snackbar close affordance`) · **Angular:** `MatSnackBar` · **Sources:** [M3 Snackbar guidelines](https://m3.material.io/components/snackbar/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Snackbars inform people about a process the app has performed or will perform. They appear temporarily towards the bottom of the screen and **don’t interrupt** — people can keep using the page.

| Need | Use |
|---|---|
| Brief, non-blocking feedback (e.g. “Changes saved”) | Snackbar |
| High-priority information that needs a decision | Dialog — blocks the app until acted on |

## Anatomy

| # | Element | Required |
|---|---|---|
| 1 | Container | Yes — opaque, with shadow |
| 2 | Text label | Yes — directly relates to the process |
| 3 | Action (text button) | No — max one |
| 4 | Close affordance (icon) | No |

## Figma component and properties

| Property | Values |
|---|---|
| Configuration | Text only, Text & action, Text & longer action |
| # of lines | One line, Two lines |
| Show close affordance | True, False |
| Supporting text | Text |

## Decision rules

1. **MUST** show only **one** snackbar at a time.
2. A snackbar MAY contain **one** action (`Configuration=Text & action` or `Text & longer action`). “Dismiss” or “Cancel” actions are optional.
3. The action **MUST** be a text button with coloured text. **MUST NOT** use a filled or elevated button.
4. Without an action → auto-dismiss after 4–10 s. With an action → stays until the person acts on it or dismisses it.
5. On medium and large screens, aim for **one line** of text with an optional action; in wide layouts, extend the container width for longer text instead of adding lines.
6. Place the snackbar at the bottom, in front of main content. **MUST NOT** cover navigation components or fully obscure actionable elements.
7. Need a decision or blocking information → use a dialog, not a snackbar.

## Behavior and interaction

- Appears and disappears automatically (no action) or stays until dismissed (with action).
- Doesn’t block interaction with the page.

## States

The action and close affordance have Enabled, Hovered, Focused and Pressed states.

## Content guidelines

- The text label directly relates to the process performed (e.g. “Auftrag gespeichert”).
- The action text **MUST** differ in colour from the label text.

## Usage guidelines

| Do | Don’t |
|---|---|
| One snackbar, one short message | Stack several snackbars |
| A single text action like “Rückgängig” | Use a filled or elevated button |
| Keep the container opaque and legible | Cover navigation or the focused element |

## Accessibility

- On web, snackbars that disappear on their own can be missed; if the message matters, add an action so it doesn’t dismiss until acted on.
- Don’t position the snackbar where it fully hides actionable or focused elements.

## AI checklist

- [ ] Non-blocking feedback → snackbar; blocking → dialog
- [ ] One snackbar, max one text action
- [ ] Auto-dismiss without action (4–10 s); persistent with action
- [ ] Bottom placement, not over navigation
- [ ] One line on larger screens

## Not covered

The exact timeout within 4–10 s is a platform/implementation decision. Set it in Angular `MatSnackBar` `duration`.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Text only | `snackBar.open('Gespeichert', undefined, { duration: 4000, panelClass: 'pdr-snackbar' })` |
| Text & action | `snackBar.open('Gelöscht', 'Rückgängig', { duration: 6000, panelClass: 'pdr-snackbar' })` |
| Longer action / two lines / close affordance | `snackBar.openFromComponent(PdrSnackbar, { data: { message, action, closable: true }, panelClass: 'pdr-snackbar' })` |

`PdrSnackbar` uses `matSnackBarLabel`, `matSnackBarActions`, `matSnackBarAction` directives and a close `matIconButton`. Position defaults to bottom-center.


Never use snackbars for errors that need action — use `../pdr/alerts.md`.

### Overrides


None — Figma matches M3 defaults. Do not add any.
