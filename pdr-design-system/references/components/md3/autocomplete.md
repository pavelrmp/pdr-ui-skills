# Autocomplete

Figma page: **Autocomplete** `10808:967` · status 🔴 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10808-967)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

> 🔴 Not final in Figma. Use Material defaults / minimal styling and flag deviations in the PR.

## Components
Page is empty in Figma. Option rows reuse **Menu list item 48** (see `menus-select.md`).

## Mapping
```html
<mat-form-field appearance="outline">
  <mat-label>Kunde</mat-label>
  <input matInput [formControl]="customer" [matAutocomplete]="auto" />
  <mat-autocomplete #auto [displayWith]="displayName" autoActiveFirstOption>
    @for (c of filtered(); track c.id) { <mat-option [value]="c">{{ c.name }}</mat-option> }
  </mat-autocomplete>
</mat-form-field>
```
Async results: debounce input (`300ms`), show `<mat-option disabled>` with `mat-progress-spinner diameter="20"` while loading.

## Overrides

None — Figma matches M3 defaults. Do not add any.
