# Chips

Figma page: **Chips** `10826:960` · status 🌕 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10826-960)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

> 🌕 Not final in Figma. Use Material defaults / minimal styling and flag deviations in the PR.

## Components
- **Assistive chip** `7320:44244` — `Style` Outlined|Elevated · `Configuration` Label only|Label & icon|Label & favicon|Label & brand icon · `State`
- **Suggestion chip** `7320:43644` — `Style` · `Selected` · `Show icon`
- **Filter chip** `7320:43825` — `Style` · `Configuration` Label only|Label & leading icon · `Selected` · `Show trailing icon`
- **Filtering chip v2** `9399:4813`, **Filter chip with clear button** `9400:5194`, **Clear filter** `9400:5183`
- **Input chip** `7320:44441` — `Configuration` Label only|Label & leading icon|Label & avatar · `Selected` · `Show closing icon`
- **Dropdown chip** `8021:8308` — `Configuration` Label only|Label & leading icon
- **Chip group** `7320:44651` — `Type` Input|Assistive|Filter|Suggestion · `Layout` Single row - scrollable|Multiple rows - overflow

32px, `corner-small`, label-large = M3 default.

## Mapping
| Figma | Angular |
|---|---|
| Assistive chip | `<mat-chip-set><mat-chip>` (with icon: `<mat-icon matChipAvatar>`) |
| Suggestion chip | `<mat-chip-set><mat-chip>` (clickable → `(click)` + `role="button"`) |
| Filter chip | `<mat-chip-listbox [multiple]="true" formControlName><mat-chip-option [value]>` ; Selected → `selected` |
| Filter chip with clear / Clear filter | `<pdr-filter-chip-clear>` (`mat-chip-option` + `matChipRemove`) |
| Input chip | `<mat-chip-grid #grid>` + `<mat-chip-row (removed)>` + `<input [matChipInputFor]="grid">`; closing icon → `<button matChipRemove>` |
| Dropdown chip | `<pdr-dropdown-chip>` = `mat-chip-option` + `[matMenuTriggerFor]` |
| Style=Elevated | `class="pdr-chip--elevated"` |
| Chip group single-row scrollable | `class="pdr-chip-set--scroll"` |
| Leading icon / favicon / brand icon | `<mat-icon matChipAvatar>` or `<img matChipAvatar>` |
| Input chip Label & avatar | `<img matChipAvatar>` / `<pdr-avatar size="s" matChipAvatar>` |
| Chip group Multiple rows | default wrapping |

```html
<mat-chip-listbox [multiple]="true" formControlName="statuses" aria-label="Status filtern">
  @for (s of statuses; track s.id) { <mat-chip-option [value]="s.id">{{ s.label }}</mat-chip-option> }
</mat-chip-listbox>
```

## Overrides (`styles/components/md3/_chips.scss`)
```scss
// Figma Style=Elevated
.pdr-chip--elevated { box-shadow: var(--mat-sys-level1); }
// Figma Chip group Layout=Single row - scrollable
.pdr-chip-set--scroll { display: flex; flex-wrap: nowrap; overflow-x: auto; scrollbar-width: none; } // put on a wrapper around the chip set
```
