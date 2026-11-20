# Tree

Figma page: **Tree 🟢** `10808:1031` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10808-1031) · Figma Spec: [`11007:2706`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11007-2706)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma component:** `Tree node` (+ two examples) · **Angular:** `<mat-tree>` with `<mat-tree-node>` / `<mat-nested-tree-node>` · **Sources:** Angular Material Tree; [M3 Lists guidelines — Expand & collapse](https://m3.material.io/components/lists/guidelines); [M3 Checkbox guidelines](https://m3.material.io/components/checkbox/guidelines)

> **M3 has no tree component.** This spec combines M3 list expand/collapse and checkbox parent–child guidance with the Figma component. Other rules are labelled **(PDR)**.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

A tree shows hierarchical data (e.g. branches → departments → employees, or folders → documents) where items can expand and collapse to reveal their children.

**Use when** the data has more than one level and people need to browse or select within the hierarchy.

**Don’t use when** (PDR)

- The data has only one level → list.
- Grouped sections of content → accordion.
- People compare attributes across many items → data grid.

## Anatomy

| # | Element | Figma |
|---|---|---|
| 1 | Indent (one step per level) | `Show indent 1–3` |
| 2 | Expand/collapse toggle | `Type=Collapsed / Expanded` |
| 3 | Checkbox | `Show checkbox` |
| 4 | Icon | `Show icon` |
| 5 | Label | `Label text` |
| 6 | Meta (count, info) | `Show meta` · `Meta` |

## Figma component and properties

| Property | Values |
|---|---|
| Type | Leaf, Collapsed, Expanded, Loading |
| State | Enabled, Hovered, Focused, Selected, Disabled (per variant set) |
| Label text · Meta | Text |
| Show icon · Show checkbox · Show meta | Toggles |
| Show indent 1 · 2 · 3 | One toggle per level below the root |

## Decision rules

1. Node without children → `Type=Leaf`; node with children → `Collapsed` or `Expanded`; children still loading → `Loading`.
2. Indent: level 1 = no indent, level 2 = `Show indent 1`, level 3 = `Show indent 1 + 2`, level 4 = `Show indent 1 + 2 + 3`. (PDR)
3. Multi-select trees use `Show checkbox`. Parent checkboxes follow the M3 parent–child rule: all children selected → Selected; some → Indeterminate; none → Unselected. Selecting a parent selects all its children.
4. Single-select trees (navigation, choosing one node) use `State=Selected` without checkboxes. (PDR)
5. **SHOULD** use icons consistently: all nodes on a level have an icon, or none do. (PDR)

## Behavior and interaction

- Selecting the toggle expands or collapses a node, in a folder-like manner, revealing or hiding its children.
- Expanding a node whose children load from the server shows `Type=Loading` until they arrive. (PDR)

## States

Enabled, Hovered, Focused, Selected, Disabled — combined with Type.

## Content guidelines (PDR)

- Labels are short names of the item; meta shows counts or a short status.

## AI checklist

- [ ] Leaf / Collapsed / Expanded / Loading chosen correctly
- [ ] Indent toggles match the level
- [ ] Checkbox parents show Indeterminate for partial selection
- [ ] Single-select trees use the Selected state, not checkboxes

## Not covered (to be defined)

- **Keyboard interaction:** arrow keys to move and expand/collapse follow Angular `mat-tree` and the ARIA tree pattern. Not documented in M3.
- **Depth:** Figma supports up to 4 levels (3 indent toggles).

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Tree | `<mat-tree [dataSource]="nodes" [childrenAccessor]="children">` |
| Type=Leaf | `<mat-tree-node matTreeNodePadding>` |
| Type=Collapsed / Expanded | node with `matTreeNodeToggle` `matIconButton` (chevron), `[isExpandable]` |
| Type=Loading | `<mat-progress-spinner diameter="24">` in place of the toggle |
| State=Selected | `class="pdr-tree-node--selected"` + `aria-selected="true"` |
| State=Disabled | `aria-disabled="true"` + `pdr-tree-node--disabled` |

### Overrides (`styles/components/md3/_tree.scss`)

```scss
.pdr-tree-node--selected { background: var(--mat-sys-secondary-container); color: var(--mat-sys-on-secondary-container); font: var(--mat-sys-title-medium); border-radius: var(--mat-sys-corner-full); }
.pdr-tree-node--disabled { color: var(--pdr-sys-on-surface-disabled); pointer-events: none; }
```
