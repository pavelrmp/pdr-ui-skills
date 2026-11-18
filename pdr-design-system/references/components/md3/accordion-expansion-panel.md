# Accordion, Expansion panel

Figma page: **Accordion, Expansion panel** `3330:106` · status 🔴 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-106)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

> 🔴 Not final in Figma. Use Material defaults / minimal styling and flag deviations in the PR.

## Components
- **Accordion item** `7749:10857` — `Position` Top|Middle|Bottom · `Expanded` False|True · `State` Enabled|Hovered

## Mapping
| Figma | Angular |
|---|---|
| Group of Accordion items | `<mat-accordion [multi]="false">` |
| Accordion item | `<mat-expansion-panel>` + `<mat-expansion-panel-header>` + `<mat-panel-title>` / `<mat-panel-description>` |
| Expanded=True | `[expanded]="true"` |
| Position Top/Middle/Bottom | handled by `mat-accordion` (corner rounding on first/last) |
| State=Hovered | native |

```html
<mat-accordion>
  <mat-expansion-panel>
    <mat-expansion-panel-header><mat-panel-title>Fahrzeugdaten</mat-panel-title></mat-expansion-panel-header>
    …
  </mat-expansion-panel>
</mat-accordion>
```
Lazy content: `<ng-template matExpansionPanelContent>`.

## Overrides

None — Figma matches M3 defaults. Do not add any.
