# Chips

Figma page: **Chips 🟢** `10826:960` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10826-960) · Figma Spec: [`10995:2657`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10995-2657)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Assistive chip`, `Filter chip`, `Input chip`, `Suggestion chip`, `Dropdown chip`, `Chip group`, PDR filter patterns (`Filtering chip v2`, `Filter chip with clear button`, `Clear filter`) · **Angular:** `<mat-chip-set>`, `<mat-chip-listbox>` / `mat-chip-option`, `<mat-chip-grid>` / `mat-chip-row` · **Sources:** [M3 Chips guidelines](https://m3.material.io/components/chips/guidelines), [Chips accessibility](https://m3.material.io/components/chips/accessibility)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Chips help people enter information, make selections, filter content, or trigger actions.

| Purpose | Chip | Example |
|---|---|---|
| Action | Assist chip | Smart or automated actions, e.g. “Add to calendar” |
| Filter | Filter chip | Filters for a collection, e.g. order status |
| Information, user-authored | Input chip | Discrete information entered by a person, e.g. a recipient |
| Information, product-authored | Suggestion chip | Dynamically generated suggestions, e.g. a suggested reply |

**Chips aren’t buttons.** Use chips to enhance the current journey with contextual, supplemental options. Actions that move people to the next or previous step **MUST** be buttons.

## Anatomy

| # | Element | Notes |
|---|---|---|
| 1 | Container | Outlined, or elevated on images |
| 2 | Label text | Required |
| 3 | Leading icon / avatar / favicon | Optional, depends on chip |
| 4 | Trailing icon | Optional — input and filter chips only (remove, dropdown) |

## Figma components and properties

| Component | Key properties |
|---|---|
| Assistive chip | Style Outlined/Elevated · Configuration Label only / Label & icon / Label & favicon / Label & brand icon · State |
| Filter chip | Style · Configuration Label only / Label & leading icon · Selected · Show trailing icon · State |
| Input chip | Configuration Label only / Label & leading icon / Label & avatar · Selected · Show closing icon · State |
| Suggestion chip | Style · Selected · Show icon · State |
| Chip group | Type Input/Assistive/Filter/Suggestion chips · Layout Single row – scrollable / Multiple rows – overflow |
| Filtering chip v2, Filter chip with clear button, Clear filter | PDR filter-panel patterns (value + dropdown + clear) |

States: Enabled, Hovered, Focused, Pressed, Dragged, Disabled (availability differs per chip).

## Decision rules

1. Pick the chip by purpose using the table above.
2. **Filter chips:**
   - Use them to filter a collection.
   - A set of filter chips is either single-select or multi-select.
   - **All chip sets on a page SHOULD use the same selection type.**
3. A filter chip MAY open a menu with more options → `Dropdown chip` / `Filtering chip v2`.
4. A single selectable filter chip MAY replace a segmented button, radio buttons or a single-select menu.
5. Use `Style=Elevated` only when the chip sits on an image or a dynamic background. **MUST NOT** elevate chips placed directly on the page.
6. Show a trailing remove icon only on input and filter chips.
7. Assist chips appear after the primary content, e.g. below a card, or persistently at the bottom of a screen.
8. (PDR) `Chip group`: use `Single row – scrollable` when space is limited (e.g. mobile), `Multiple rows – overflow` when chips may wrap.

## Behavior and interaction

- Filter chip suggestions MAY change dynamically as filters are selected.
- Selecting a filter chip toggles it. In single-select sets, selecting one deselects the others.
- Input chips can be removed. A chip with two actions (select + remove) has separate targets for each.

## States

Enabled, Hovered, Focused, Pressed, Dragged and Disabled, combined with Selected True/False where the chip is selectable.

## Content guidelines

- Labels **SHOULD** be 20 characters or fewer and use the button typography style.
- Skip articles and filler words to keep labels short.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use chips for contextual, supplemental options | Replace major actions with chips |
| Keep labels short | Write labels longer than 20 characters |
| Elevate chips only over images | Elevate chips on a plain page |
| Use one selection type per page | Mix single- and multi-select chip sets on one page |

## Accessibility

- Every chip **MUST** have a 48 × 48 px target, even if the target extends beyond the visible chip.
- A trailing remove icon **MUST** have its own 48 × 48 px target that doesn’t interfere with the chip’s main action. Apply a min chip width of 88 px (or 42 px label) to make room.
- The chip label needs at least 3:1 contrast with the background.
- A chip that performs an action has button semantics.
- Labels: the remove icon is labelled “Remove {chip content}”; a chip with two actions reads “{chip content}”, then “Remove {chip content}”.
- Keyboard:
  - **Tab** moves to the chip or chip group.
  - **Space** or **Enter** selects or deselects the focused chip in multi-select sets.
  - **Backspace** or **Delete** removes the focused input chip.

## AI checklist

- [ ] Chip type matches the purpose (action, filter, input, suggestion)
- [ ] No step-to-step navigation with chips — use buttons
- [ ] Labels ≤ 20 characters
- [ ] Elevated only over images
- [ ] Same selection type for all chip sets on the page
- [ ] 48 px targets, including the remove icon

## Not covered by M3 (PDR conventions)

- **PDR filter patterns:** `Filtering chip v2`, `Filter chip with clear button` and `Clear filter` (a value chip with dropdown and clear) are PDR additions for filter panels.
- **Chip overflow on mobile:** filter rows with many chips scroll horizontally. Whether extra chips collapse into one “Filter (n)” chip is still to be decided.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Assistive chip | `<mat-chip-set><mat-chip>` (with icon: `<mat-icon matChipAvatar>`) |
| Suggestion chip | `<mat-chip-set><mat-chip>` (clickable → `(click)` + `role="button"`) |
| Filter chip | `<mat-chip-listbox [multiple]="true" formControlName><mat-chip-option [value]>` ; Selected → `selected` |
| Filter chip with clear / Clear filter | `<pdr-filter-chip-clear>` (`mat-chip-option` + `matChipRemove`) |
| Input chip | `<mat-chip-grid #grid>` + `<mat-chip-row (removed)>` + `<input [matChipInputFor]="grid">`; closing icon → `<button matChipRemove>` |
| Dropdown chip | `<pdr-dropdown-chip>` = `mat-chip-option` + `[matMenuTriggerFor]` |
| Style=Elevated | `class="pdr-chip--elevated"` |
| Chip group single-row scrollable | `class="pdr-chip-set--scroll"` |
| Leading icon / favicon / brand icon | `<mat-icon matChipAvatar>` or `<img matChipAvatar>` |
| Input chip Label & avatar | `<img matChipAvatar>` / `<pdr-avatar size="s" matChipAvatar>` |
| Chip group Multiple rows | default wrapping |

```html
<mat-chip-listbox [multiple]="true" formControlName="statuses" aria-label="Status filtern">
  @for (s of statuses; track s.id) { <mat-chip-option [value]="s.id">{{ s.label }}</mat-chip-option> }
</mat-chip-listbox>
```

### Overrides (`styles/components/md3/_chips.scss`)

```scss
// Figma Style=Elevated
.pdr-chip--elevated { box-shadow: var(--mat-sys-level1); }
// Figma Chip group Layout=Single row - scrollable
.pdr-chip-set--scroll { display: flex; flex-wrap: nowrap; overflow-x: auto; scrollbar-width: none; } // put on a wrapper around the chip set
```
