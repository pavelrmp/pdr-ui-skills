# Navigation menu (PDR)

Figma page: **Navigation menu (PDR)** `3330:118` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-118)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Side nav drawer mobile** `4104:16118` — `Menu` Main|Settings|Vorgänge
- **Side nav drawer current** `7771:10358`
- **Menu medium item** `3952:4074` — `Badge` None|Small|Large · `State` Enabled|Hovered|Pressed|Selected
- **Menu small item** `3952:4480` — `State` · `Badge`; **Menu small 2nd** `3952:4455`
- **Menu banner** `10697:48027` — `Type` AI-Funktionen|Testzeitraum
- **Menu divider** `3501:343`

Material layer (drawer container, list item heights, active indicator) → `../md3/navigation-drawer-rail.md`.

## API
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
