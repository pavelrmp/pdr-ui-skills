# Bottom sheet

Figma page: **Bottom sheet 🟢** `10998:34890` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10998-34890) · Figma Spec: [`11009:3511`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11009-3511)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Bottom sheet`, `Example/Bottom sheet` (Type Modal / Standard) · **Angular:** `MatBottomSheet` · **Sources:** [M3 Bottom sheets guidelines](https://m3.material.io/components/bottom-sheets/guidelines), [M3 Layout — Panes](https://m3.material.io/foundations/layout/scaffold/panes), [Side sheets guidelines](https://m3.material.io/components/side-sheets/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Bottom sheets show secondary content anchored to the bottom of the screen.

| Type | Use |
|---|---|
| Standard bottom sheet | Secondary content that people use **together with** the main content, without blocking it |
| Modal bottom sheet | Content that **must be interacted with or dismissed**; blocks all other app functionality. **Mobile apps only.** |

Modal bottom sheets MAY be used instead of menus to present additional actions on mobile.

**Don’t use** a modal bottom sheet on desktop — use a menu, dialog or side sheet. Side sheets suit wider screens; bottom sheets suit compact screens.

## Anatomy

| # | Element | Notes |
|---|---|---|
| 1 | Container | Anchored to the bottom edge |
| 2 | Drag handle | Optional — drag or select to change the sheet height |
| 3 | Scrim | Modal only |

## Figma components

| Component | Property | Values / use |
|---|---|---|
| Bottom sheet | Show drag handle | True (default) — shows the 32 × 4 px handle |
| Bottom sheet | Show headline · Headline | Optional title above the content |
| Bottom sheet | Content (slot) | Any content; default is an action list (`Menu list item 56`) |
| Example/Bottom sheet | Type | Modal (scrim, ≤ 50 % height), Standard (no scrim) |

Tokens: `surface-container-low`, top corners `--mat-sys-corner-extra-large` (28 px), elevation level 1. On mobile the sheet fills the screen width.

## Decision rules

1. The person must act on or dismiss the content → **modal** (with scrim); they keep working with the page → **standard**.
2. **MUST** use modal bottom sheets in mobile layouts only.
3. The initial height of a modal bottom sheet **MUST NOT** exceed **50 %** of the screen height.
4. Provide a drag handle when the sheet has several heights. If a sheet has preset heights but no drag handle, **MUST** offer a single-pointer alternative to change the height.

## Behavior and interaction

- Modal bottom sheets appear in front of app content and stay until confirmed, dismissed, or a required action is taken.
- Dragging or selecting the drag handle moves the sheet between preset heights.
- A bottom sheet MAY be docked to a window edge to show additional actions (pane layouts).

## Usage guidelines

| Do | Don’t |
|---|---|
| Use a modal bottom sheet for actions on mobile | Use modal bottom sheets on desktop |
| Start modal sheets at ≤ 50 % height | Open a modal sheet covering most of the screen |
| Offer a drag handle or alternative for height | Hide height changes behind gestures only |

## AI checklist

- [ ] Mobile only for modal bottom sheets
- [ ] Modal vs standard chosen by whether it blocks the page
- [ ] Initial height ≤ 50 %
- [ ] Drag handle or a single-pointer alternative

## Not covered (to be defined when the component is built)

- **Preset heights:** not modelled in Figma.
- **Scrim:** uses `sys/scrim` (`--mat-sys-scrim`) at 32 % opacity.
- **Spacing:** drag handle (16 px top, 8 px bottom) and header (16 px) spacing are PDR choices, not confirmed M3 values.
- When PDR uses a bottom sheet instead of a side sheet on tablet.

---

# Part 2 — Angular implementation

### Mapping
| Figma | Angular |
|---|---|
| Example/Bottom sheet · Type=Modal | `MatBottomSheet.open(Component, { panelClass: 'pdr-bottom-sheet', ariaLabel })` — **mobile layouts only** (`PDR_BREAKPOINTS.mobile`) |
| Type=Standard | Not a Material component: a fixed container docked to the bottom of the page (`.pdr-standard-sheet`), no scrim |
| Show drag handle | `<button class="pdr-bottom-sheet__handle" aria-label="Höhe ändern">` — also the single-pointer alternative for changing height |
| Show headline | `<h2 class="pdr-bottom-sheet__title">` (`--mat-sys-title-large`) |
| Content (default action list) | `<mat-nav-list>` with `<a mat-list-item (click)="ref.dismiss(action)">` |

```ts
private sheet = inject(MatBottomSheet);
openActions() {
  if (!this.bp.isMatched(PDR_BREAKPOINTS.mobile)) return this.openMenu(); // desktop: use a menu instead
  this.sheet.open(OrderActionsSheet, { panelClass: 'pdr-bottom-sheet', ariaLabel: 'Aktionen' });
}
```

### Overrides (`styles/components/md3/_bottom-sheet.scss`)
```scss
// Container color (surface-container-low) and 28 px top corners are the M3 defaults — don't override them.
.pdr-bottom-sheet { max-height: 50dvh; box-shadow: var(--mat-sys-level1); }   // spec: initial height ≤ 50 %
.pdr-bottom-sheet__handle {
  display: block; width: 32px; height: 4px; padding: 0; border: 0;
  margin: var(--pdr-space-16) auto var(--pdr-space-8);
  border-radius: var(--mat-sys-corner-full);
  background: var(--mat-sys-on-surface-variant); opacity: .4;
}
.pdr-bottom-sheet__title { font: var(--mat-sys-title-large); margin: 0 var(--pdr-space-16) var(--pdr-space-16); }
```
