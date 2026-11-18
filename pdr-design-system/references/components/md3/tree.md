# Tree

Figma page: **Tree** `10808:1031` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10808-1031)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Tree node** `10810:1248` — `Type` Leaf|Collapsed|Expanded|Loading · `State` Enabled|Hovered|Selected|Disabled · 48px, body-large (Selected: title-medium)

## Mapping
| Figma | Angular |
|---|---|
| Tree | `<mat-tree [dataSource]="nodes" [childrenAccessor]="children">` |
| Type=Leaf | `<mat-tree-node matTreeNodePadding>` |
| Type=Collapsed / Expanded | node with `matTreeNodeToggle` `matIconButton` (chevron), `[isExpandable]` |
| Type=Loading | `<mat-progress-spinner diameter="24">` in place of the toggle |
| State=Selected | `class="pdr-tree-node--selected"` + `aria-selected="true"` |
| State=Disabled | `aria-disabled="true"` + `pdr-tree-node--disabled` |

## Overrides (`styles/components/md3/_tree.scss`)
```scss
.pdr-tree-node--selected { background: var(--mat-sys-secondary-container); color: var(--mat-sys-on-secondary-container); font: var(--mat-sys-title-medium); border-radius: var(--mat-sys-corner-full); }
.pdr-tree-node--disabled { color: var(--pdr-sys-on-surface-disabled); pointer-events: none; }
```
