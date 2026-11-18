# Skeleton loaders, empty and error states

Figma page: **Skeleton loaders, empty and error states** `10808:1015` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10808-1015)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Skeleton** `10811:985` — `Shape` Text|Heading|Circle|Rectangle|Button|Chip · `Effect` Static|Shimmer
- **Skeleton list item** `10811:1005` — `Lines` 1|2|3; **Skeleton card** `10811:1006`, **Skeleton paragraph** `10811:1014`, **Skeleton table row** `10811:1020`
- **Empty state illustration** `10812:983` — `Type` MFA|IP address|Email|Calculation|Notes|Pending|Customer|Vehicle
- **Empty state/No data** `10812:984`, **Empty state/No results** `10814:997`
- **Error state/Failed loading** `10814:1024`, **Error state/No connection** `10814:1052`

## API
```html
<pdr-skeleton shape="text|heading|circle|rectangle|button|chip" effect="shimmer" />
<pdr-skeleton-list-item [lines]="2" />  <pdr-skeleton-card />  <pdr-skeleton-paragraph />  <pdr-skeleton-table-row [cols]="6" />
<pdr-empty-state type="no-data|no-results" [illustration]="'customer'" (action)="create()" />
<pdr-error-state type="failed-loading|no-connection" (retry)="reload()" />
```
## Tokens
Skeleton fill `--mat-sys-surface-container-high`, shimmer highlight `--mat-sys-surface-container-low`; shapes use matching corner tokens (text `corner-extra-small`, button/chip `corner-full`/`corner-small`, circle `corner-full`). Shimmer disabled under `prefers-reduced-motion`.
Empty/error: illustration (SVG via MCP `download_assets`), title-large, body-medium on-surface-variant, primary action `matButton="filled"` / retry `matButton="outlined"`.

## A11y
Skeleton container `aria-busy="true"` + visually-hidden "Wird geladen"; individual skeletons `aria-hidden="true"`.
