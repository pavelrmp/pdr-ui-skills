# State layers

Figma: **⚛️ Design Tokens** page `3313:3` · [Design Tokens page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3313-3)
Machine-readable source: `../../tokens.json`. Theme setup: `../theming-rules.md`.

Interaction states are a translucent layer of the content color (`on-*` role) on top of the component. Figma variables `state-layer/*/Opacity-8 · 12 · 16`. Angular Material applies them automatically — only custom `pdr-*` components need them by hand.

| State | Opacity | CSS |
|---|---|---|
| Hover | 8 % | `--mat-sys-hover-state-layer-opacity` |
| Focus | 12 % (+ 2 px focus ring for custom elements) | `--mat-sys-focus-state-layer-opacity` |
| Pressed | 12 % | `--mat-sys-pressed-state-layer-opacity` |
| Dragged | 16 % | `--mat-sys-dragged-state-layer-opacity` |
| Disabled content | 38 % opacity | — (Material handles it) |
| Disabled container | 12 % of `on-surface` | — (Material handles it) |

## PDR helpers

| CSS | Value | Use |
|---|---|---|
| `--pdr-state-layer-on-surface-8` | `on-surface` at 8 % | Table row hover, custom list rows |
| `--pdr-state-layer-on-surface-12` | `on-surface` at 12 % | Custom pressed / focused rows |
| `--pdr-state-layer-on-surface-16` | `on-surface` at 16 % | Custom dragged items |

```scss
.pdr-megaoption { position: relative; }
.pdr-megaoption::after { content: ''; position: absolute; inset: 0; border-radius: inherit; background: var(--mat-sys-on-surface); opacity: 0; pointer-events: none; }
.pdr-megaoption:hover::after { opacity: var(--mat-sys-hover-state-layer-opacity); }
.pdr-megaoption:active::after, .pdr-megaoption:focus-visible::after { opacity: var(--mat-sys-pressed-state-layer-opacity); }
.pdr-megaoption:focus-visible { outline: 2px solid var(--mat-sys-primary); outline-offset: 2px; }
```
