# App shell

Figma: **Example/App shell** `10723:15611` · `Breakpoint` Mobile | Tablet | Desktop · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10723-15611)

## Structure

```
page (surface)
├── App bar             pdr-app-bar          64 px, padding 8/0, surface
├── Page header         pdr-page-header      desktop/tablet 80 px (pad 16/24/16/24) · mobile 60 px (pad 16/16/8/16)
└── Container           .pdr-page-container  pad 0/24/24/24 (≥ M) · 0/16/24/16 (< M), gap 8
    └── Panel           pdr-panel            surface-container-lowest, corner-large, max-width 1128
        ├── Panel title MD3                  56 px (pad 8/8/0/16)
        ├── Content                          pad 0/16/16/16
        └── Pagination container             pad-top 24 (optional)
```

| Breakpoint | Frame | Panel width | Notes |
|---|---|---|---|
| Desktop | 1600 | 1128 max | Page header "Desktop and Tablet" |
| Tablet | 992 | fluid (944) | same header |
| Mobile | 375 | fluid (343) | Page header "Mobile", container padding 16 |

## Angular

```html
<!-- app.component.html -->
<pdr-app-bar />
<main class="pdr-page"><router-outlet /></main>
```
```html
<!-- any page -->
<pdr-page-header title="Aufträge">
  <ng-container pdrPageHeaderActions><button matButton="filled">Neuer Auftrag</button></ng-container>
</pdr-page-header>
<div class="pdr-page-container">
  <pdr-panel>
    <pdr-panel-title>Übersicht</pdr-panel-title>
    …
  </pdr-panel>
</div>
```
```scss
@use 'pdr/breakpoints' as *;
.pdr-page { min-height: 100dvh; background: var(--mat-sys-surface); }
.pdr-page-container {
  display: flex; flex-direction: column; gap: var(--pdr-space-8);
  padding: 0 var(--pdr-space-16) var(--pdr-space-24);
  @include pdr-up(m) { padding: 0 var(--pdr-space-24) var(--pdr-space-24); }
  > * { width: 100%; max-width: 1128px; }
}
```
## Rules
- One `pdr-page-header` per page. The page's primary action sits in the header on desktop/tablet and becomes a FAB on mobile (see `data-grid-page.md`).
- Content always lives inside panels — never directly on `surface`.
