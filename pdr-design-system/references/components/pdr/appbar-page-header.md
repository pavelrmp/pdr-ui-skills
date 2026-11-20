# Appbar & Page header

Figma page: **Appbar & Page header 🟢** `3330:116` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-116) · Figma Spec: [`11032:4514`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11032-4514)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `App bar`, `Page header`, `Breadcrumbs`, `Section title`, `Example/Page header`, order header parts (`Order title`, `Suborders`, `Order title and suborders`, `Task buttons`), menus (`Settings menu basic`, `Second-level menu`, `Header actions`) · **Angular:** `pdr-app-bar`, `pdr-page-header` (title input, actions slot); others custom (selectors to confirm) · **Sources:** component descriptions on this page (App bar, Page header and Breadcrumbs are 🔒 LOCKED); [M3 App bars](https://m3.material.io/components/app-bars/guidelines) for context

> **No M3 component.** App bar and Page header are PDR components and **locked**: rules from their descriptions are mandatory. Other rules marked **(PDR proposal — confirm)**.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

| Component | Purpose |
|---|---|
| App bar | Global application header on every page: logo, user, main navigation, notifications |
| Page header | Context of the current page: page title, breadcrumbs (deep pages) and page-level actions |
| Breadcrumbs | Path to the current page — only inside the Page header |
| Section title | Title of a section or panel inside the page, with optional icons and a count |
| Example/Page header | Reference configurations for typical page types |

## Figma components and properties

| Component | Properties |
|---|---|
| App bar | Size: Desktop, Tablet, Mobile · Version: v 2026 · Show beta |
| Page header | Size: Desktop and Tablet, Mobile · Text (page title) · Show breadcrumbs |
| Breadcrumbs | — (fixed design) |
| Section title | Show leading icon + Left Icon · Show trailing icon + Right Icon · Show number |
| Example/Page header | Page type: Processes, Planning co-pilot, Order |

## Decision rules

**App bar (🔒 locked)**

1. **MUST** use the App bar exactly as provided on every page. **MUST NOT** change layout, colours, sizes, spacing, icons or order, or add/remove elements.
2. Choose `Size` by screen size (Desktop / Tablet / Mobile). The only other option is `Show beta`.
3. The elevation (level 1) and the shadow are part of the design — **MUST NOT** be removed or changed.
4. The logo is always the SVG layer inside the component — never PNG/JPG, never redrawn.

**Page header (🔒 locked)**

1. **Only two things change per page:** the page title text and the page-level actions on the right.
2. Title typography: Desktop and Tablet = display small (36/44); Mobile = headline medium (28/36).
3. **Breadcrumbs:** hidden by default; **MUST** be shown only on pages at the 3rd navigation level or deeper (e.g. Aufträge › Auftrag A-0001 › Kalkulation). Levels 1 and 2 never show breadcrumbs.
4. **Page-level actions:**
   - **Desktop:** secondary actions sit on the right side of the primary action, same button size.
   - **Tablet:** secondary actions hidden in a ⋮ icon button next to the primary action.
   - **Mobile:** the primary action becomes a FAB; secondary actions go into the ⋮ menu.
5. Start from `Example/Page header` when the page type matches (Processes, Planning co-pilot, Order).

**Section title**

1. (PDR proposal — confirm) Use `Section title` for sections and panels inside a page — never as a page title. `Show number` shows the count of items in the section.

## Behavior and interaction

- Breadcrumbs are derived from the router in Angular and appear automatically from level 3.
- App bar navigation and notifications behave the same on every page.

## AI checklist

- [ ] App bar unchanged, Size by screen
- [ ] Page header: only title and actions changed
- [ ] Breadcrumbs only from level 3
- [ ] Actions: right of primary (desktop) · ⋮ (tablet) · FAB + ⋮ (mobile)
- [ ] Section title only inside the page

## Open questions for the team

- **Deprecated layers:** `App bar`, `Page header`, `Example/Page header`, `Header actions`, `Order title`, `Suborders`, `Order title and suborders` and `Task buttons` still contain `Deprecated/Button`. App bar and Page header are 🔒 locked — swapping the button needs an explicit decision.
- **Unused components:** `Header actions`, `Settings menu basic` and `Second-level menu` have no uses in this file. Are they still needed?
- **Order header parts:** `Order title`, `Suborders`, `Order title and suborders` and `Task buttons` were recovered from an old library. `Order title` and `Suborders` still use a default “Property 1” property. Should they be completed or merged into the Order page header example?

---

# Part 2 — Angular implementation

### 🔒 Locked components


**App bar** and **Page header** are locked: their design cannot be changed. This is stated in the Figma component descriptions too. Claude must never restyle, rearrange, extend or "improve" them — no new elements, colors, sizes, spacing or order, no per-page variants.

#### App bar `9329:6038`
- Use the one shared `<pdr-app-bar />` on every page, exactly as designed. It has **no styling inputs**.
- Allowed configuration only: `Size` (Desktop / Tablet / Mobile — chosen automatically by breakpoint) and `Show beta` (`[beta]="true"`).
- **Elevation is part of the design**: the app bar always has elevation **level 1** (Figma effect style `M3/Elevation Light/1`, `Dark/1` in dark mode). The shadow cannot be removed, reduced or changed — not on scroll, not per page.
  ```scss
  // inside pdr-app-bar only
  :host { display: block; background: var(--mat-sys-surface); box-shadow: var(--mat-sys-level1); position: relative; z-index: 2; }
  ```
  `--mat-sys-level1` switches between the light and dark shadow automatically (see `../../theming-rules.md`).
- **Logo is an SVG and ships with this skill: `assets/brand/pdr-logo.svg`** (44 × 44, exported from the Logo layer of the App bar in Figma; identical in Desktop, Tablet and Mobile). Always use this file — never a placeholder, never ask the user to export it, never PNG/JPG, never rebuilt with CSS, text or icon fonts.
  - Angular: copy it to `src/assets/brand/pdr-logo.svg` and embed it: `<img src="assets/brand/pdr-logo.svg" alt="PDR.cloud" width="44" height="44">` (or inline the SVG markup).
  - Designs / mockups / HTML prototypes: inline the SVG markup from the file directly.
  - Its colors (`#1D75E8` background, white mark) are part of the brand asset and are the only allowed hard-coded colors.
  - If the logo changes in Figma, re-export the Logo layer (select it → Export → SVG) and replace the file in the skill.

#### Page header `10125:1535`
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

### Mapping

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
| Settings menu / Second-level menu | `mat-menu` | see `../md3/menu.md` |
| Order title / Suborders | `<pdr-order-title>` | `mat-chip-listbox` for suborders |
| Footer | `<pdr-footer>` | body-small, on-surface-variant |

### Tokens

Background `--mat-sys-surface`, title `--mat-sys-on-surface`, icons `--mat-sys-on-surface-variant`, spacing `--pdr-space-16/24`.
