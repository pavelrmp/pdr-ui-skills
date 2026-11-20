# Dialogs

Figma page: **Dialogs 🟢** `3330:117` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-117) · Figma Spec: [`10997:2654`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10997-2654)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Basic dialog`, `Dialog with scrollable content`, `Dialog title`, `Dialog title and description`, `Dialog content`, `Dialog actions`, `Full-screen dialog header`, `Dialog toolbar` · **Angular:** `MatDialog` (`mat-dialog-title`, `mat-dialog-content`, `mat-dialog-actions`) · **Sources:** [M3 Dialogs guidelines](https://m3.material.io/components/dialogs/guidelines), [Dialogs specs](https://m3.material.io/components/dialogs/specs), [Snackbar — similar components](https://m3.material.io/components/snackbar/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

A dialog is a modal window in front of app content that provides critical information or asks for a decision. Dialogs disable all app functionality while they’re open and stay on screen until confirmed, dismissed, or a required action is taken.

**Use when** the person must make a decision or acknowledge urgent information before continuing.

**Don’t use when**

- The message is about a process and needs no decision → snackbar.
- Options can be offered without interrupting → a dropdown menu is less disruptive.
- Dialogs are purposefully interruptive — **use them sparingly**.

## Variants

| M3 variant | Figma | Use |
|---|---|---|
| Basic dialog | `Basic dialog` (Screen size Tablet and Desktop / Mobile), `Dialog with scrollable content` | Urgent information, details or actions; lets people confirm, dismiss or acknowledge |
| Full-screen dialog | `Full-screen dialog header` + content | A series of tasks to complete (e.g. creating an entry with several fields) on compact screens |

On expanded screens (840 px and wider), use a basic dialog instead of a full-screen dialog.

## Anatomy (basic dialog)

| # | Element | Required | Figma |
|---|---|---|---|
| 1 | Container | Yes | `Basic dialog` |
| 2 | Icon | No | `Dialog title and description` (Icon) |
| 3 | Headline | No | `Dialog title` · Title |
| 4 | Supporting text | Yes | Supporting text / `Dialog content` |
| 5 | Divider | No | Between scrolling content and actions |
| 6 | Actions | Yes | `Dialog actions` |

Full-screen dialog: container, header with close icon, headline, text button (e.g. Save), optional divider.

## Figma properties

| Component | Properties |
|---|---|
| Dialog title / Dialog title and description | Title, Supporting text, Show supporting text, Show info + Info text, Show trailing icon, Vertical or Icon |
| Dialog actions | Actions: 1 button, 2 buttons, 3 buttons, With a comment, delete + 3 buttons |
| Full-screen dialog header | Screen size Mobile / Desktop, Show button, Show button 2 |
| Dialog with scrollable content | Device Desktop and Tablet / Mobile, content slot |

## Decision rules

1. Decision or urgent information → basic dialog; a multi-field task on mobile → full-screen dialog.
2. **MUST** provide a way to confirm and/or dismiss; dialogs stay until one of these happens.
3. Full-screen dialog: the confirming action is **Save**. **MUST NOT** use the confirming action to dismiss.
4. When someone dismisses a full-screen dialog with unsaved changes, **MUST** show a basic dialog to confirm discarding them.
5. Only full-screen dialogs can have other dialogs on top of them. A basic dialog **MUST NOT** be covered by anything else.
6. Long content → `Dialog with scrollable content`, with a divider between content and actions.

## Behavior and interaction

- Dialogs appear and disappear with an enter/exit transition.
- While open, the rest of the app is blocked (modal) behind a scrim.

## Content guidelines

- (PDR) Headline: a clear question or statement. Supporting text: what happens and why.
- Action labels name the result (e.g. “Löschen”, “Abbrechen”), not “Yes/No”. *(PDR wording)*

## Usage guidelines

| Do | Don’t |
|---|---|
| Use dialogs for decisions that block the flow | Use a dialog for non-blocking status — use a snackbar |
| Confirm discarding unsaved changes in full-screen dialogs | Dismiss a full-screen dialog with its Save action |
| Use a basic dialog on large screens | Use full-screen dialogs on expanded screens |

## Combining with other components

- **Buttons:** the dialog actions use the button rules (Buttons spec); the most important action gets the higher emphasis.
- **Date and time pickers:** these open as dialogs and are confirmed with OK.

## Measurements (basic dialog)

| Attribute | Value |
|---|---|
| Corner radius | 28 px |
| Width | Min 280 px, max 560 px |
| Padding (all sides) | 24 px |
| Space between buttons | 8 px |
| Title to body | 16 px |
| Icon to title | 16 px |
| Body to actions | 24 px |
| Icon size | 24 px |
| Alignment | Centered with an icon, start-aligned without |
| Divider height | 1 px |

## AI checklist

- [ ] A dialog is really needed (blocking decision), otherwise snackbar or menu
- [ ] Basic on desktop and tablet; full-screen only for multi-step tasks on compact screens
- [ ] Clear confirm/dismiss actions
- [ ] Unsaved full-screen changes are confirmed before discarding
- [ ] Width 280–560 px, 24 px padding, 28 px radius

## Not covered by M3 (PDR conventions)

- **`Dialog actions` variants:** “With a comment” and “delete + 3 buttons” are PDR patterns.
- **`Dialog toolbar`:** a recovered PDR component.
- **Keyboard behavior** (e.g. Esc to close) and focus handling: not listed in the sources used here. Follow Angular `MatDialog` defaults.

---

# Part 2 — Angular implementation

### Overrides (`styles/components/md3/_dialogs.scss`)


```scss
@use '@angular/material' as mat;

html {
  // Figma <Paper>: surface-container-lowest + level5 (M3: surface-container-high, no shadow)
  @include mat.dialog-overrides((
    container-color: var(--mat-sys-surface-container-lowest),
    container-elevation-shadow: var(--mat-sys-level5),
  ));
}
.pdr-dialog--mobile     { @include mat.dialog-overrides((container-shape: var(--mat-sys-corner-large))); }
.pdr-dialog--fullscreen { @include mat.dialog-overrides((container-shape: 0, container-elevation-shadow: none)); }
.pdr-dialog__title--center { text-align: center; }
.pdr-spacer { flex: 1 1 auto; }
```
