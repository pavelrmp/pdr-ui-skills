# Settings page

Figma: **Example/Settings page** `10724:30020` · `Breakpoint` Desktop | Tablet | Mobile · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10724-30020)
Built on `app-shell.md` (app bar, page header, content container). Grid/breakpoints: `../foundations/grids-breakpoints.md`.

## Desktop (1600)
```
App bar · Page header (pad 16/24)
Section (row, pad 24, gap 24)
├── Menu (265 px, vertical, gap 2)
│   └── Navigation drawer items (56 px, corner-full) + expanded 2nd level
└── Column (fluid, max 839, gap 16)
    └── Panels (surface-container-lowest, corner-large) — one per settings group
```

## Tablet (768) & Mobile (375)
The menu becomes **tabs** under the page header (`nav mat-tab-nav-bar`, 48 px + 1 px outline-variant divider). Panels stack in one column (pad 16, gap 16). The last block is a button column (pad 16/0) with save/cancel.

## Angular
```html
<pdr-page-header title="Einstellungen" />
@if (isDesktop()) {
  <div class="pdr-settings">
    <mat-nav-list class="pdr-sidenav pdr-settings__menu">
      @for (s of sections; track s.path) {
        <a mat-list-item [routerLink]="s.path" routerLinkActive #r="routerLinkActive" [activated]="r.isActive">{{ s.label }}</a>
      }
    </mat-nav-list>
    <div class="pdr-settings__content"><router-outlet /></div>
  </div>
} @else {
  <nav mat-tab-nav-bar [tabPanel]="tp" mat-stretch-tabs="false">…</nav>
  <mat-tab-nav-panel #tp class="pdr-settings__content"><router-outlet /></mat-tab-nav-panel>
}
```
```scss
.pdr-settings { display: flex; gap: var(--pdr-space-24); padding: var(--pdr-space-24); }
.pdr-settings__menu { flex: 0 0 265px; }
.pdr-settings__content { flex: 1 1 auto; max-width: 839px; display: flex; flex-direction: column; gap: var(--pdr-space-16); }
```
## Rules
- Each settings group = one `pdr-panel` with `pdr-panel-title`. Toggles use the Form switcher (`../components/md3/switch.md`), selects `../components/md3/menus-select.md`.
- Save per panel **or** one sticky action bar — never both on the same page.
