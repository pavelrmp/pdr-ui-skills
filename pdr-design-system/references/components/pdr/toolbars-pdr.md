# Toolbars (PDR)

Figma page: **Toolbars (PDR)** `3330:120` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-120)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Order toolbar** `5044:25992`, **Order toolbar compact** `3693:5156`, **Order header toolbar** `5176:11740`
- **Filter calculation** `6151:9994`, **Filter graphic calculation** `6145:14141`

Material layer → `../md3/toolbar.md` (`pdr-toolbar` class).

| Figma | Wrapper | Built from |
|---|---|---|
| Order toolbar / compact | `<pdr-order-toolbar [order] [compact]>` | `mat-toolbar.pdr-toolbar` + status tag + `matButton`s; compact collapses secondary actions into a kebab `mat-menu` |
| Order header toolbar | `<pdr-order-header>` | `pdr-order-title` + suborders + `pdr-avatar-group` |
| Filter calculation / graphic | `<pdr-filter-bar>` | `mat-chip-listbox` filter chips + `pdr-dropdown-chip` + `pdr-search-bar` + clear `matButton` |

Overflow rule: on < L (992px) move all but the primary action into `mat-menu`.
