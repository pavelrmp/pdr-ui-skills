# Appbar & Page header

Figma page: **Appbar & Page header** `3330:116` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-116)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **App bar** `9329:6038` — `Version` v 2026 · `Size` Desktop|Tablet|Mobile (+ legacy **App bar mobile** `4104:21868`, **App bar tablet** `4104:21825`)
- **Top app bar** `5126:14156` — `Configuration` Small centered|Small|Medium|Large · `Elevation` flat|on-scroll
- **Page header** `10125:1535` — `Size` Desktop and Tablet|Mobile
- **Breadcrumbs** `3513:3670`, **Section title** `3317:94`, **Header actions** `8851:20492`, **Footer** `3642:7851`
- **Settings menu basic** `3558:2890`, **Second-level menu** `4798:1021`
- **Order title** `10917:39575`, **Suborders** `10917:39618`

## 🔒 Locked components

**App bar** and **Page header** are locked: their design cannot be changed. This is stated in the Figma component descriptions too. Claude must never restyle, rearrange, extend or "improve" them — no new elements, colors, sizes, spacing or order, no per-page variants.

### App bar `9329:6038`
- Use the one shared `<pdr-app-bar />` on every page, exactly as designed. It has **no styling inputs**.
- Allowed configuration only: `Size` (Desktop / Tablet / Mobile — chosen automatically by breakpoint) and `Show beta` (`[beta]="true"`).
- **Logo is an SVG**: 44 × 44 (instance in the app bar: `9768:5050`). Export it from Figma as SVG (select the logo → Export → SVG, or Figma MCP export of node `9768:5050`) into `src/assets/brand/pdr-logo.svg`. Embed it as SVG (`<img src="assets/brand/pdr-logo.svg" alt="PDR.cloud" width="44" height="44">` or an inline SVG component). Never PNG/JPG, never rebuilt with CSS, text or icon fonts.

### Page header `10125:1535`
Only **two things change per page**:
1. the **page title** (`title` input, rendered as the page's only `<h1>`)
2. the **page-level actions** on the right side (projected into `pdrPageHeaderActions`)

Everything else (layout, height, typography, spacing, breadcrumb position) is fixed. No subtitle, no extra content, no custom styles.

**Page title typography** (same as MD3):
| Size | Text style | Token |
|---|---|---|
| Desktop and Tablet | display small (Roboto 36/44) | `font: var(--mat-sys-display-small)` |
| Mobile | headline medium (Roboto 28/36) | `font: var(--mat-sys-headline-medium)` |

```scss
// inside pdr-page-header only — pages never style the title
.pdr-page-header__title {
  margin: 0;
  font: var(--mat-sys-headline-medium);
  letter-spacing: var(--mat-sys-headline-medium-tracking);
  color: var(--mat-sys-on-surface);
  @include pdr-up(m) {
    font: var(--mat-sys-display-small);
    letter-spacing: var(--mat-sys-display-small-tracking);
  }
}
```
The switch happens at the M breakpoint (768 px), where the Figma variant changes from Mobile to Desktop and Tablet.

**Breadcrumbs are hidden by default.** They appear only when the page is on the **3rd navigation level or deeper** (e.g. Aufträge › Auftrag A-0001 › Kalkulation). Level 1 and 2 pages never show them. Pages don't decide this themselves: `pdr-page-header` derives the trail from the router.

**Page-level actions (right side):**
| Size | Rule |
|---|---|
| Desktop | Primary action plus secondary actions to its right, same button size |
| Tablet | Primary action + secondary actions in a ⋮ (`more_vert`) `matIconButton` menu |
| Mobile | Primary action becomes a FAB (`pdr-fab--primary`, see `../../examples/data-grid-page.md`); secondary actions go into the ⋮ menu (more than 3 → menu button) |

```html
<pdr-page-header title="Kalkulation">
  <ng-container pdrPageHeaderActions>
    <button matButton="filled">Speichern</button>
    <button matButton="outlined">Exportieren</button>
  </ng-container>
</pdr-page-header>
```
```ts
// inside pdr-page-header: breadcrumbs from route data, shown from level 3
// routes: { path: 'orders', data: { breadcrumb: 'Aufträge' }, children: [{ path: ':id', data: { breadcrumb: 'Auftrag' }, children: [...] }] }
private router = inject(Router);
trail = toSignal(this.router.events.pipe(
  filter(e => e instanceof NavigationEnd), startWith(null),
  map(() => buildTrail(this.router.routerState.snapshot.root)), // [{ label, url }] for each route with data.breadcrumb
), { initialValue: [] });
showBreadcrumbs = computed(() => this.trail().length >= 3);
```

## Mapping
| Figma | Wrapper | Built from |
|---|---|---|
| App bar (v 2026) 🔒 | `<pdr-app-bar [beta]>` (no other inputs) | `mat-toolbar`, `matIconButton` (menu, notifications with `matBadge`), `pdr-avatar` + `mat-menu` (account) |
| Size=Desktop/Tablet/Mobile | responsive inside `pdr-app-bar` via `BreakpointObserver` (M 768 / L 992) | — |
| Top app bar Small / Small centered / Medium / Large | `<pdr-top-app-bar size="small|center|medium|large">` | `mat-toolbar`; title: title-large (small) / headline-small (medium) / headline-medium (large) |
| Elevation=on-scroll | `[elevateOnScroll]="true"` → surface-container + level2 when scrolled (`CdkScrollable`) | — |
| Page header 🔒 | `<pdr-page-header [title]>` with `pdrPageHeaderActions` slot — nothing else is configurable | title: `display-small` (desktop/tablet) / `headline-medium` (mobile), `matButton`s |
| Breadcrumbs | rendered **only by `pdr-page-header`**, from level 3; never placed on a page directly | `<nav aria-label="Brotkrümel"><ol>` + `routerLink`, last item `aria-current="page"` |
| Section title | `<pdr-section-title>` | title-medium + optional action `matButton` |
| Header actions | `pdrPageHeaderActions` content | `matButton`, `matIconButton`, `mat-menu` |
| Settings menu / Second-level menu | `mat-menu` | see `../md3/menus-select.md` |
| Order title / Suborders | `<pdr-order-title>` | `mat-chip-listbox` for suborders |
| Footer | `<pdr-footer>` | body-small, on-surface-variant |

## Tokens
Background `--mat-sys-surface`, title `--mat-sys-on-surface`, icons `--mat-sys-on-surface-variant`, spacing `--pdr-space-16/24`.
