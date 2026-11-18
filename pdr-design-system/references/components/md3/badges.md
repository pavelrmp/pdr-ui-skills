# Badges

Figma page: **Badges** `10745:46595` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10745-46595)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Badge** `4494:31913` — `Size` Small|Large|XLarge · fill `sys/semantic/error/error`, `corner-full`, label-small

## Mapping
| Figma | Angular |
|---|---|
| Size=Small (6px dot) | `matBadge="" matBadgeSize="small"` |
| Size=Large (16px, 1–2 digits) | `[matBadge]="count"` (default size) |
| Size=XLarge (auto width, e.g. "99+") | `[matBadge]="count > 99 ? '99+' : count"` (default size grows) |
| Hidden at 0 | `[matBadgeHidden]="count === 0"` |

Always add `matBadgeDescription` for screen readers. Color is `error` by default in M3 — no `matBadgeColor`.

## Overrides

None — Figma matches M3 defaults. Do not add any.
