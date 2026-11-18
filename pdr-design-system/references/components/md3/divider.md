# Divider

Figma page: **Divider** `10808:983` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10808-983)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Divider** `10816:979` — `Orientation` Horizontal|Vertical · `Inset` None|Inset|Middle inset · color outline-variant
- **Divider with subheader** `10816:980`

## Mapping
| Figma | Angular |
|---|---|
| Horizontal | `<mat-divider>` |
| Vertical | `<mat-divider [vertical]="true">` (parent must stretch height) |
| Inset=Inset | `[inset]="true"` (inside `mat-list`) |
| Inset=Middle inset | `class="pdr-divider--middle"` |
| Divider with subheader | `<mat-divider>` + `<div mat-subheader>Title</div>` |

## Overrides (`styles/components/md3/_divider.scss`)
```scss
// Figma Inset=Middle inset (16px both sides)
.pdr-divider--middle { margin-inline: var(--pdr-space-16); }
```
