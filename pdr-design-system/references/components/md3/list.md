# List

Figma page: **List 🟢** `10998:40436` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10998-40436) · Figma Spec: [`11009:3606`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11009-3606)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `List item`, `List`, `Example/List` · **Angular:** `<mat-list>`, `<mat-nav-list>`, `<mat-selection-list>` + `<mat-list-option>` · **Sources:** [M3 Lists guidelines](https://m3.material.io/components/lists/guidelines), [Divider guidelines](https://m3.material.io/components/divider/guidelines), [Checkbox](https://m3.material.io/components/checkbox/guidelines) and [Radio button](https://m3.material.io/components/radio-button/guidelines) guidelines

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Lists show a vertical set of items with text and optional visuals, so people can scan, open or select items.

(PDR) **Use when** items share one main attribute and are scanned one after another (people, documents, settings, mobile versions of tables).

(PDR) **Don’t use when** people compare several attributes across many items → Table (Data Grids) on larger screens.

## Anatomy

| # | Element | Required |
|---|---|---|
| 1 | Container | **Yes** |
| 2 | Label text | **Yes** |
| 3 | Supporting text | No |
| 4 | Trailing text | No |
| 5 | Leading visual (icon, avatar, avatar text, image) | No |
| 6 | Trailing visual (icon, checkbox, radio button, switch) | No |
| 7 | Divider | No |

## Variants by content

| Content | Notes |
|---|---|
| Label text only | One line; if it doesn’t fit, it wraps or truncates |
| Label + supporting text (one line) | — |
| Label + supporting text (two or more lines) | Limit supporting text to 1–3 lines; truncate depending on screen size |

## Figma components

| Component | Property | Values / use | Angular |
|---|---|---|---|
| List item | Lines | 1 (56 px), 2 (72 px), 3 (88 px; leading/trailing top-aligned) | — |
| List item | State | Enabled, Hovered (8 %), Focused (12 % + ring), Pressed (12 %), Disabled (38 %) | — |
| List item | Label text · Supporting text | Label: 1 line; supporting: 1 line (Lines=2) or 2 lines (Lines=3), truncated | `matListItemTitle` · `matListItemLine` |
| List item | Show leading · Leading | Swap: icon (24), Avatar (40), Checkbox, Radio button, Switch | `matListItemIcon` / `matListItemAvatar` |
| List item | Show trailing · Trailing · Show trailing text · Trailing text | Swap: icon, Checkbox, Radio button, Switch; short trailing text (time, count) | `matListItemMeta` |
| List item | Show divider | Full-width divider at the bottom | `<mat-divider>` |
| List | Show subheader · Subheader · Items (slot) | Container for List items | `<mat-list>`, `<mat-nav-list>`, `<mat-action-list>`, `<mat-selection-list>` |
| Example/List | Type | Navigation, Multi-select, Single-select, Contacts | — |

Spacing: 16 px left / 24 px right padding, 16 px between elements.

## Decision rules

1. **MUST** include container and label text; everything else is optional.
2. Keep label text brief. Limit supporting text to one to three lines.
3. Align supporting visuals and primary text in every item so the list is easy to scan.
4. Multi-select list → checkboxes. Single-select list → radio buttons, **not** checkboxes. A switch MAY toggle a standalone setting in a list item.
5. Group items with **segmented gaps** and filled list items, or with dividers: inset dividers between related items, full-width dividers between groups.
6. Items that contain other items MAY expand and collapse (folder-like) to reveal or hide content.

## Behavior and interaction

- Selecting an item opens it, or selects it in selection lists.
- Expandable items reveal and hide their children.

## States

Enabled, Hovered, Focused, Pressed, Disabled (`State`). Selection is shown by the checkbox or radio button in the item.

## Usage guidelines

| Do | Don’t |
|---|---|
| Keep labels brief and aligned | Let visuals and text start at different positions |
| Use checkboxes for multi-select, radio buttons for single-select | Use checkboxes in a single-select list |
| Group with gaps or dividers | Put a divider between every item when spacing is enough |

## AI checklist

- [ ] Container + label text in every item
- [ ] Supporting text ≤ 3 lines
- [ ] Visuals and text aligned
- [ ] Correct selection control (checkbox / radio / switch)
- [ ] Groups via gaps or dividers, not dividers everywhere

## Not covered (to be defined when the component is built)

- **Dragged state** (reordering) and **image/video leading content** aren’t modelled yet.
- PDR mobile list-item rules (key field first, amount trailing) are in **Table (Data Grids) › Tables on mobile devices**.

---

# Part 2 — Angular implementation

### Mapping
| Figma | Angular |
|---|---|
| Example/List · Navigation | `<mat-nav-list>` + `<a mat-list-item routerLink>` |
| List of actions | `<mat-action-list>` + `<button mat-list-item>` |
| Example/List · Multi-select | `<mat-selection-list>` + `<mat-list-option togglePosition="before">` (checkboxes) |
| Example/List · Single-select | `<mat-selection-list [multiple]="false">` (radio indicator) |
| Example/List · Contacts / read-only | `<mat-list>` + `<mat-list-item>` |
| Lines=1 / 2 / 3 | `lines="1|2|3"` on the item (56 / 72 / 88 px) |
| Label text · Supporting text | `<span matListItemTitle>` · `<span matListItemLine>` |
| Leading icon · Avatar | `<mat-icon matListItemIcon>` · `<pdr-avatar matListItemAvatar size="40">` |
| Trailing visual · Trailing text | `<span matListItemMeta>` (switch: `<mat-slide-toggle>` inside the meta slot) |
| Show divider | `<mat-divider>` between groups (inset: `[inset]="true"`) |
| Show subheader | `<div mat-subheader>` |
| State=Disabled | `[disabled]="true"` on the item / option |

```html
<mat-nav-list>
  <div mat-subheader>Kunden</div>
  @for (c of customers(); track c.id) {
    <a mat-list-item lines="2" [routerLink]="['/customers', c.id]">
      <pdr-avatar matListItemAvatar size="40" [category]="c.category" [name]="c.name" />
      <span matListItemTitle>{{ c.name }}</span>
      <span matListItemLine>{{ c.city }}</span>
      <span matListItemMeta>{{ c.openOrders }}</span>
    </a>
  }
</mat-nav-list>
```

### Overrides

None — Figma matches M3 defaults. Do not add any.
