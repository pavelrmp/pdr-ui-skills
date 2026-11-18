# Cards

Figma page: **Cards** `10826:959` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10826-959)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Card** `10829:1397` — `Style` Elevated|Filled|Outlined · `State` Enabled|Hovered|Pressed|Dragged|Disabled · 12px radius (`corner-medium`), header title-medium

| Style | Container | Border | Shadow |
|---|---|---|---|
| Elevated | surface-container-low | — | level1 |
| Filled | surface-container-highest | — | — |
| Outlined | surface | outline-variant | — |

## Mapping
| Figma | Angular |
|---|---|
| Style=Elevated | `<mat-card appearance="raised">` |
| Style=Filled | `<mat-card appearance="filled">` |
| Style=Outlined | `<mat-card appearance="outlined">` |
| Header / media / actions | `<mat-card-header>` (`mat-card-avatar`, `<mat-card-title>`, `<mat-card-subtitle>`), `<img mat-card-image>`, `<mat-card-content>`, `<mat-card-actions align="end">` |
| State=Hovered/Pressed (clickable card) | wrap card in `<a>`/`<button class="pdr-card--interactive">`; never put `(click)` on `mat-card` |
| State=Dragged | `cdkDrag` on the card; `cdkDragPreview` gets level4 |
| State=Disabled | `aria-disabled="true"` + `pdr-card--disabled` on wrapper |

## Overrides (`styles/components/md3/_cards.scss`)
```scss
.pdr-card--interactive { display: block; border-radius: var(--mat-sys-corner-medium); text-decoration: none; color: inherit; }
.pdr-card--interactive:focus-visible { outline: 2px solid var(--mat-sys-primary); outline-offset: 2px; }
.pdr-card--disabled { opacity: .38; pointer-events: none; }
```
Container colors/shape = M3 defaults — do not override.
