# Sheets (side sheets)

Figma page: **Sheets 🟢** `5197:5440` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=5197-5440) · Figma Spec: [`10999:2794`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10999-2794)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Side Sheet` (content slot), `Example/Side sheet` (Summary 1, Forms 1, Timeline, Forms 2), `Example/Order planning` (Tab: Rental car, Order Info) · **Angular:** side sheet as `<mat-sidenav position="end">`; bottom sheet via `MatBottomSheet` · **Sources:** [M3 Side sheets guidelines](https://m3.material.io/components/side-sheets/guidelines), [Chips guidelines](https://m3.material.io/components/chips/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Side sheets show secondary content anchored to the side of the screen.

| Type | Use |
|---|---|
| Standard side sheet | Content that complements the screen’s main content **without blocking** it (e.g. details of a selected item next to a list) |
| Modal side sheet | Content in front of the app that **blocks** other functionality until confirmed, dismissed, or a required action is taken (e.g. filter controls) |

**Use when** secondary content or controls relate to the current screen and people benefit from keeping the main content in view.

**Don’t use when** (PDR) the content is a blocking decision → dialog; it’s top-level navigation → navigation drawer.

## Anatomy

**Standard:** container · headline · close icon button · divider (optional).

**Modal:** container · headline · close icon button · back icon button (optional) · divider (optional) · action buttons (optional) · scrim.

## Figma components and properties

| Component | Property | Use |
|---|---|---|
| Side Sheet | Slot | Put the sheet content into the slot |
| Example/Side sheet | Example: Summary 1, Forms 1, Timeline, Forms 2 | Start points for typical PDR sheets |
| Example/Order planning | Tab: Rental car, Order Info | PDR order-planning sheet |

## Decision rules

1. People must keep working with the main content → **standard** side sheet.
2. The sheet holds a task that must be completed or dismissed first (e.g. filters, a form) → **modal** side sheet with a scrim.
3. Modal side sheets on smaller screens MAY become standard side sheets on larger screens.
4. Use a divider to separate action buttons from content, or user-generated from system-generated content.
5. Many filter chips → organise them in a side sheet.
6. **MUST** provide a close icon button. A back icon button is optional (PDR: use it for multi-level content).

## Behavior and interaction

- **Modal side sheets** disable all other app functionality and stay until confirmed, dismissed, or a required action is taken.
- **Standard side sheets** let people use the sheet and the main content at the same time.

## States

No component states. Contained components use their own states.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use standard sheets for complementary details | Block the page with a sheet when it isn’t necessary |
| Use modal sheets for filters and short forms | Put top-level navigation in a side sheet |
| Separate actions from content with a divider | Leave a sheet without a close button |

## AI checklist

- [ ] Standard (non-blocking) vs modal (blocking + scrim) chosen correctly
- [ ] Close button present; back button only for nested content
- [ ] Divider between content and actions
- [ ] Not used for navigation or blocking decisions

## Not covered (to be defined)

- **Bottom sheets:** described in M3, but there’s no Figma component yet.
- **Sheet width, header layout and action placement:** not modelled as Figma properties. Follow the Example components.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Side Sheet `8161:21398` (500w) | Route-level: `<mat-sidenav position="end" mode="over">` inside `mat-sidenav-container`. Programmatic: `<pdr-side-sheet>` opened via `MatDialog` with `position: { right: '0' }`, `height: '100dvh'`, `panelClass: ['pdr-dialog', 'pdr-side-sheet']` |

Side sheet tokens: surface-variant, start corners `corner-large`, level3.

### Overrides (`styles/components/md3/_sheets.scss`)

```scss
@use '@angular/material' as mat;
.pdr-side-sheet {
  @include mat.dialog-overrides((
    container-color: var(--mat-sys-surface-variant),
    container-shape: var(--mat-sys-corner-large) 0 0 var(--mat-sys-corner-large),
    container-elevation-shadow: var(--mat-sys-level3),
  ));
}
```

Bottom sheets have their own page and file: `bottom-sheet.md`.
