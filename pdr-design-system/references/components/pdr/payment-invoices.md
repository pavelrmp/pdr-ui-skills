# Payment & Invoices

Figma page: **Payment & Invoices** `3330:124` · status 🌕 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-124)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

> 🌕 Not final in Figma. Use Material defaults / minimal styling and flag deviations in the PR.

## Components
- **Invoice accordion** `8143:24137` — `Expanded` · `State`
- **Invoice status** `10917:40116`, **Invoice check status** `10917:40172` — `State` yellow|green|AI, **Invoice delivery status** `10917:40139` — `State` Yellow|Green
- **Invoice arrows** `10917:40076` — `Status arrow` Success|Warning|Error
- **Invoice price chip** `10917:41893`, **Invoice tooltip** `10917:41902`, **Selected cell** `10917:40100`
- **Delivery note mapping table with toolbar** `10917:36042`
- **Receipt PDF** `3720:1421`, **Repair cost approval (RKÜ)** `6538:6881`

## Mapping
| Figma | Wrapper | Built from |
|---|---|---|
| Invoice accordion | `<pdr-invoice-accordion>` | `mat-expansion-panel` (see `../md3/accordion-expansion-panel.md`) |
| Invoice status / check / delivery status | `pdr-check-status`, `pdr-delivery-status` | see `status-tags.md` (Check status / Delivery status) — same component, invoice context |
| Invoice arrows | `<pdr-status-arrow status="success|warning|error">` | icon in `--pdr-sys-success` / `--pdr-sys-warning` / `--mat-sys-error` |
| Invoice price chip | `pdr-price-chip` | see `status-tags.md` |
| Invoice tooltip | `pdr-rich-tooltip` | see `../md3/tooltips.md` |
| Delivery note mapping table | `mat-table` + `pdr-toolbar` | Selected cell → `pdr-cell--selected` (primary-container) |
| Receipt PDF | `<pdr-pdf-viewer>` | embedded viewer in `pdr-panel` |
| Repair cost approval (RKÜ) | `<pdr-rku-form>` | form fields + `mat-table` |

Amounts: `CurrencyPipe` with `'EUR'` and `de-DE`, `font-variant-numeric: tabular-nums`, right-aligned.
