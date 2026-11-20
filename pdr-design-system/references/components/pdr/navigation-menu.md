# Navigation menu

Figma page: **Navigation menu (PDR) 🟢** `3330:118` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-118) · Figma Spec: [`10998:38628`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10998-38628)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Navigation drawer`, `Navigation drawer item`, `Menu medium item`, `Menu divider`, `Menu banner` · **Angular:** `<mat-sidenav-container>` + `<mat-sidenav>` with `<mat-nav-list>` · **Sources:** [M3 Navigation drawer guidelines](https://m3.material.io/components/navigation-drawer/guidelines), [Navigation drawer accessibility](https://m3.material.io/components/navigation-drawer/accessibility), [M3 Navigation rail guidelines](https://m3.material.io/components/navigation-rail/guidelines), [Navigation bar](https://m3.material.io/components/navigation-bar/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Navigation drawers and rails let people move between the top-level destinations of the app.

| Component | Use |
|---|---|
| Standard navigation drawer | Large and desktop screens; sits next to content. Permanently visible drawers allow quick navigation between unrelated destinations. |
| Modal navigation drawer | Mobile screens; opens over content with a scrim |
| Navigation rail | Medium screens and larger; a vertical bar of destinations on the leading edge |
| Navigation bar | Compact screens (mobile) with 3–5 destinations — not on this page |

## Anatomy

| # | Element | Notes |
|---|---|---|
| 1 | Container (sheet) | Drawer or rail |
| 2 | Navigation item | Icon + label |
| 3 | Active indicator | Background shape behind the current destination |
| 4 | Icon | Supplements the label |
| 5 | Label | Required in drawers |
| 6 | Badge | Optional (counts, updates) |
| 7 | Section label / headline | Optional, groups destinations |
| 8 | Divider | Optional, between groups |

## Figma components and properties

| Component | Properties |
|---|---|
| Navigation drawer | Menu: Vorgänge, Planung, Lager, Finanzen, Docs, Sonstiges, Rail (one per app area; Rail = collapsed rail) · Screen size: Desktop and Tablet, Mobile |
| Navigation drawer item | State: Enabled, Hovered, Pressed, Selected · Level: 1st, 2nd · Label text · Show icon · Icon · Show arrow · Show badge notification · Left / Right Icon |
| Menu medium item | Rail item (icon + label): State: Enabled, Hovered, Pressed, Selected · Badge: None, Small, Large · Show label text · Label text · Icon |
| Menu divider | Divider between groups of destinations |
| Menu banner | Type: AI-Funktionen, Testzeitraum — promotional banner at the bottom of the drawer |

## Decision rules

1. Choose by screen size:
   - **Compact (mobile)** → modal drawer, or a navigation bar.
   - **Medium** → navigation rail.
   - **Large and desktop** → standard drawer.
2. **MUST** show exactly one destination as active (`State=Selected`): active indicator + filled icon + more prominent colour. **MUST NOT** show the active indicator on more than one item.
3. Unselected destinations use outlined icons; the selected one uses the filled icon.
4. Separate **groups** of destinations with full-width dividers; **MUST NOT** put dividers between individual destinations.
5. Badges: on a rail, place them at the upper right of the icon (collapsed) or next to the label (expanded).
6. Rail: **MUST** run vertically on the leading edge; never horizontal (use a navigation bar instead).
7. An expanded rail opens from a menu icon and MAY reveal secondary destinations.

## Behavior and interaction

- **Tap/click:** the active indicator appears on the selected item with a ripple, and the icon switches from outlined to filled.
- **Hover:** a hover indicator shows that the destination is interactive.
- **Rail scrolling:** destinations stay fixed while content scrolls vertically. If content scrolls horizontally underneath, separate the rail with a divider or elevation.
- **Modal drawer:** opens over content with a scrim. (PDR) It closes when a destination is chosen or the scrim is tapped.

## States

Navigation item: Enabled, Hovered, Pressed, Selected (active).

## Content guidelines

- Icons supplement the labels. (PDR) Labels are short and name the destination.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use a modal drawer on mobile, standard on large screens | Use a standard drawer on mobile |
| Show one active destination | Highlight several items at once |
| Separate groups with dividers | Put dividers between single destinations |

## Accessibility

- People **MUST** be able to move between destinations with assistive technology and select one.
- The selected destination uses a filled icon, not only colour, so selection is clear without colour.

## PDR navigation rules

1. Choose the `Navigation drawer` by app area (`Menu`) and screen size; `Menu=Rail` for the collapsed rail.
2. Rail destinations use `Menu medium item`; drawer destinations use `Navigation drawer item`.
3. Badges on rail items: `Badge=Small` for an update, `Badge=Large` for a count (see Badges).
4. Separate groups with `Menu divider` — never between single destinations (M3 rule above).
5. (PDR proposal — confirm) `Menu banner` at most once, at the bottom of the drawer: `AI-Funktionen` to promote AI features, `Testzeitraum` to show the remaining trial days.

## AI checklist

- [ ] Component chosen by screen size (modal / rail / standard)
- [ ] Exactly one item Selected, with a filled icon
- [ ] Dividers only between groups
- [ ] Rail vertical on the leading edge
- [ ] Badges placed per rule

## Not covered by M3 (PDR conventions)

- **Drawer Types per app area** (Verwaltung, Lager, Finanzen, …) are PDR content presets.
- **`Level=2nd`** (nested destinations) and **`Show arrow`** are PDR additions.
- **Side nav drawer mobile** and other PDR variants live on “Navigation menu (PDR)”.

## Open questions for the team

- **Deprecated layers:** `Navigation drawer`, `Menu banner` and `Side nav drawer current` still contain `Deprecated/Button`. Swap to the current Button.
- **Leftover value:** `Navigation drawer` has a variant `Menu=Property 214`. Rename or remove it.
- **Unused component:** `Side nav drawer current` has no uses. Is it the current drawer, or can it be archived?

---

# Part 2 — Angular implementation

### API

```html
<pdr-side-nav [items]="nav" [collapsed]="rail()">
  <pdr-menu-banner pdrSideNavFooter type="ai" />
</pdr-side-nav>
```
| Figma | Implementation |
|---|---|
| Menu medium item | `<pdr-nav-item size="medium" [badge]>` = `a mat-list-item` + icon |
| Menu small item / small 2nd | `size="small"` / nested (`pdr-nav-item--nested`) |
| Badge=Small / Large | `matBadge` dot (`matBadgeSize="small"`) / count |
| State=Selected | `routerLinkActive` → `[activated]` + `aria-current="page"` |
| Side nav drawer mobile Menu=Main/Settings/Vorgänge | `mat-sidenav mode="over"` with drill-down panels (`@if` per menu level + back `matIconButton`) |
| Menu banner AI-Funktionen / Testzeitraum | `<pdr-menu-banner type="ai|trial">` — `mat-card appearance="filled"` with `--mat-sys-tertiary-container` (ai) / `--mat-sys-primary-container` (trial) + `matButton` |
| Menu divider | `<mat-divider>` |

### Material layer — drawer & rail

| Figma | Angular |
|---|---|
| Navigation drawer | `<mat-sidenav-container>` + `<mat-sidenav [mode]="isDesktop ? 'side' : 'over'" [opened]>` |
| Side Nav medium (rail) | `pdr-sidenav--rail` (collapsed width, icons only + `matTooltip`) |
| Navigation drawer item Level 1st | `<a mat-list-item routerLink routerLinkActive #rla="routerLinkActive" [activated]="rla.isActive">` in `<mat-nav-list>` |
| Level 2nd | same + `class="pdr-nav-item--nested"` |
| State=Selected | `[activated]` (secondary-container) + `aria-current="page"` |
| Section labels | `<div mat-subheader>` |

### Overrides (`styles/components/md3/_navigation-menu.scss`)

```scss
@use '@angular/material' as mat;
.pdr-sidenav {
  // Figma drawer item: 56px, fully rounded
  @include mat.list-overrides((
    list-item-one-line-container-height: 56px,
    active-indicator-shape: var(--mat-sys-corner-full),
    active-indicator-color: var(--mat-sys-secondary-container),
  ));
}
.pdr-nav-item--nested { padding-inline-start: var(--pdr-space-48); }
```
