# Tooltips

Figma page: **Tooltips** `10745:46756` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10745-46756)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Plain tooltip** `3736:1469` — inverse-surface, `corner-extra-small`, body-small, padding 4/8
- **Rich tooltip** `10098:9303` — surface-container, `corner-medium`, level2, 312w

## Mapping
| Figma | Angular |
|---|---|
| Plain tooltip `3736:1469` | `matTooltip="…"` (`matTooltipPosition` as designed). Defaults match. |
| Rich tooltip `10098:9303` | `<pdr-rich-tooltip>` via `cdkConnectedOverlay`: surface-container, `corner-medium`, level2, title-small heading + body-medium + optional text `matButton` actions |

Tooltips never hold the only copy of essential information; icon-only triggers still need `aria-label`.


```html
<button matIconButton matTooltip="Bearbeiten" aria-label="Bearbeiten"><mat-icon fontSet="material-symbols-outlined">edit</mat-icon></button>
```
Onboarding hints → `../pdr/popovers-tipseens.md`.

## Overrides (`styles/components/md3/_tooltips.scss`)
```scss
.pdr-rich-tooltip {
  background: var(--mat-sys-surface-container);
  border-radius: var(--mat-sys-corner-medium);
  box-shadow: var(--mat-sys-level2);
  max-width: 312px;
  padding: var(--pdr-space-12) var(--pdr-space-16) var(--pdr-space-8);
}
```
Plain tooltip = M3 default.
