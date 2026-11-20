# Expansion panel

Figma page: **Expansion panel 🟢** `3330:106` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-106) · Figma Spec: [`10993:2741`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10993-2741)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma component:** `Accordion item` (draft) · **Angular:** `<mat-accordion>` with `<mat-expansion-panel>` · **Sources:** [M3 Lists guidelines — Expand & collapse](https://m3.material.io/components/lists/guidelines), [M3 Cards guidelines — Dividers](https://m3.material.io/components/cards/guidelines), [M3 Layout — Showing & hiding](https://m3.material.io/foundations/layout/layout-overview/adaptive-design)

> **M3 has no dedicated accordion or expansion-panel component.** This spec only uses M3 guidance on expanding and collapsing content, plus the properties of the draft Figma component. Everything else is listed under “Not covered”.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

An accordion groups content under headers that expand and collapse, so people can reveal or hide content in place. M3 describes the same pattern for lists: list items that contain other items can expand and collapse in a folder-like manner, to reveal or hide content.

**Use when**

- Related sections of content are optional to read and would make the page too long if all were open.
- The layout must show or hide information to fit the available space.

**Don’t use when** (PDR proposal — not defined in M3)

- People need to compare content across sections at the same time → show it openly or use tabs.
- There is a single block of extra detail → open a detail page or a dialog instead.

## Anatomy

| # | Element | Required | Notes |
|---|---|---|---|
| 1 | Header | Yes | Title, expand/collapse indicator |
| 2 | Leading icon | No | `Show leading icon` |
| 3 | Delete action | No | `Show delete` |
| 4 | Content | Yes, when expanded | Revealed below the header |
| 5 | Divider | No | Full-width dividers indicate content that can expand (M3 Cards) |

## Figma component and properties

| Property | Values | Use / Angular |
|---|---|---|
| Position | Top, Middle, Bottom | First, middle and last item in a stacked group |
| Expanded | False, True | Collapsed or open; expanded panels detach with rounded corners, the arrow points up |
| State | Enabled, Hovered (8 %), Focused (12 % + ring), Disabled (38 %, collapsed only) | Disabled = `[disabled]`; a disabled panel can’t be opened |
| Title | Text | `<mat-panel-title>` |
| Show description · Description | Toggle / text | `<mat-panel-description>` |
| Show leading icon · Left Icon Instance | Toggle / icon swap | Optional icon before the title |
| Show delete | Toggle | Delete action (Icon button) |
| Content | Instance swap | The expanded body |

## Decision rules

1. Stack items in a group: the first item gets `Position=Top`, items in between `Position=Middle`, the last `Position=Bottom`.
2. (PDR proposal) Show sections collapsed (`Expanded=False`) by default unless the first section is the main content.
3. **SHOULD** use full-width dividers to mark content that can expand.
4. (PDR proposal) Use `Show delete` only when the section represents an item the person can remove.

## Behavior and interaction

- Selecting the header toggles `Expanded`.
- When expanding, content is revealed below the header and pushes following items down.

## States

Enabled, Hovered, Focused, Disabled (`State`) — combined with Expanded True/False. Disabled exists only collapsed.

## Content guidelines

- (PDR proposal) Titles are short and describe the content of the section.
- (PDR proposal) Don’t nest an accordion inside another accordion.

## AI checklist

- [ ] Content is optional and benefits from being hidden
- [ ] Positions set correctly (Top, Middle, Bottom)
- [ ] (PDR) Collapsed by default unless it’s the main content
- [ ] (PDR) No nested accordions

## Not covered by M3 (to be defined)

- **Single vs. multiple open sections:** in Angular, `multi` on `mat-accordion` controls this. M3 gives no guidance.
- **Keyboard and screen-reader behavior:** no M3 guidance in the sources used here.
- **Measurements and tokens:** no M3 values exist for this component.
- **Action row** (`mat-action-row`) and toggle position (before/after) aren’t modelled.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Group of Accordion items | `<mat-accordion [multi]="false">` |
| Accordion item | `<mat-expansion-panel>` + `<mat-expansion-panel-header>` + `<mat-panel-title>` / `<mat-panel-description>` |
| Expanded=True | `[expanded]="true"` |
| Position Top/Middle/Bottom | handled by `mat-accordion` (corner rounding on first/last) |
| State=Hovered | native |

```html
<mat-accordion>
  <mat-expansion-panel>
    <mat-expansion-panel-header><mat-panel-title>Fahrzeugdaten</mat-panel-title></mat-expansion-panel-header>
    …
  </mat-expansion-panel>
</mat-accordion>
```
Lazy content: `<ng-template matExpansionPanelContent>`.

### Overrides


None — Figma matches M3 defaults. Do not add any.
