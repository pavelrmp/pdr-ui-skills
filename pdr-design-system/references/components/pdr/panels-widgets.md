# Panels & Widgets

Figma page: **Panels & Widgets** `3330:121` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-121)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Panel** `8689:3153` — surface-container-lowest, `corner-large`, 688w
- **Panel title** `3642:7340`, **Panel title interactive** `7101:63116`, **Panel title MD3** `8679:8815`
- **Start page widget template** `8706:4157`, **Slider widgets mobile** `6172:34733`
- **Slider arrows** `5603:11734` — `Style` Filled|Ghost|Outlined

## API
```html
<pdr-panel>
  <pdr-panel-title [interactive]="true" (click)="expand()">Offene Aufgaben
    <button matIconButton pdrPanelAction aria-label="Mehr"><mat-icon fontSet="material-symbols-outlined">more_vert</mat-icon></button>
  </pdr-panel-title>
  …
</pdr-panel>
```
| Figma | Implementation |
|---|---|
| Panel | `:host { background: var(--mat-sys-surface-container-lowest); border-radius: var(--mat-sys-corner-large); padding: var(--pdr-space-16); }` |
| Panel title / MD3 | title-medium (MD3 variant: title-large) + actions slot |
| Panel title interactive | whole title is a `<button>` with state layer + chevron |
| Start page widget template | `<pdr-widget>` = `pdr-panel` with fixed header/footer slots in a CSS grid dashboard |
| Slider widgets mobile | horizontal scroll-snap container (`scroll-snap-type: x mandatory`) |
| Slider arrows Filled / Outlined / Ghost | `matIconButton` + `pdr-icon-btn--filled` / `--outlined` / default (see `../md3/buttons.md`) |
