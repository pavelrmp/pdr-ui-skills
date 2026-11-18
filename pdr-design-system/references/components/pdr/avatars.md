# Avatars

Figma page: **Avatars** `3562:3774` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3562-3774)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Avatar** `3562:3976` — `Category` Privatkunde|Geschäftskunde|Autohaus|Sachverständiger|Rechtsanwalt|Versicherung|PDR Bot|Monogram
- **Avatar size/S·M·L·XL·XXL** `8892:18057…18061`, **Substitute avatar** `9789:11872`, **PDR logo 24** `10917:32793`
- **Avatar group** `8956:212` — `Type` Placeholder|Initials|Mix
- **Selected user** `8881:15092` — `State` Enabled|Hovered|Pressed

## API
```html
<pdr-avatar category="autohaus" size="m" [name]="customer.name" [src]="customer.photoUrl" />
<pdr-avatar-group [users]="team" [max]="4" size="s" />
<pdr-selected-user [user]="assignee" (click)="openPicker()" />
```
| Figma | Input |
|---|---|
| Category=X | `category="privatkunde|geschaeftskunde|autohaus|sachverstaendiger|rechtsanwalt|versicherung|bot|monogram"` → category icon + color |
| Monogram | initials from `name` |
| Substitute avatar | fallback when `src` fails |
| Size S/M/L/XL/XXL | `size="s|m|l|xl|xxl"` — read exact px from the `Avatar size/*` nodes via MCP |
| Avatar group Type | overflow chip "+N" when `users.length > max` |
| Selected user | `<button>` with state layer (on-surface 8/12%), `corner-full` |

## Tokens
Shape `--mat-sys-corner-full`; category backgrounds use `--pdr-sys-*-container` / text `--pdr-sys-on-*-container` (assign one extended color per category, verify with design); group overlap `-8px` + 2px `--mat-sys-surface` ring.

## A11y
Decorative avatar next to a name → `alt=""`; standalone → `alt`/`aria-label` = person name.
