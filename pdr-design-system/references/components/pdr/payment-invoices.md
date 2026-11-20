# Payment & Invoices

Figma page: **Payment & Invoices 🌕** `3330:124` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-124) · Figma Spec: [`11037:9976`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11037-9976)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🌕 In progress · **Figma components:** `Invoice accordion`, `Delivery note mapping table with toolbar`, `Invoice status`, `Invoice delivery status`, `Invoice check status`, `Invoice price chip`, `Invoice arrows`, `Selected cell`, `Invoice tooltip`, `Receipt PDF`, `Repair cost approval (RKÜ)` · **Angular:** custom PDR components (selectors to confirm) · **Sources:** components on this page; PDR Status tags and Data Grids rules

> **No M3 component.** Most components were recovered from an old library. Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Payment & Invoices covers checking supplier invoices and delivery notes against orders: mapping delivery-note lines to invoice lines, checking prices, and showing the check status of each line.

## Figma components and properties

| Component | Properties / use |
|---|---|
| Invoice accordion | Size: Desktop · Expanded: False, True · State: Enabled, Hovered — one invoice with its lines |
| Delivery note mapping table with toolbar | Size: Mapping table desktop — table mapping delivery-note lines to invoice lines |
| Invoice status | Status: Nicht geprüft |
| Invoice delivery status | State: Yellow, Green · Flow: Col 1 |
| Invoice check status | State: yellow, green, AI |
| Invoice price chip | State: Default — a price value in a line |
| Invoice arrows | Status arrow: Success, Warning, Error — price change indicator |
| Selected cell · Invoice tooltip | Property 1: Default · Property 1: Bottom |
| Receipt PDF · Repair cost approval (RKÜ) | Document previews |

## Decision rules

1. The mapping table follows the **Data Grids** rules (numbers right-aligned, header divider, no table border, hover and selection).
2. Status colours follow the **Status tags** colour rules (container / on container / icon); don’t invent new status colours.
3. (PDR proposal — confirm) `Invoice arrows`: Success = price as expected or lower, Warning = small deviation, Error = price higher than agreed.
4. (PDR proposal — confirm) `Invoice check status · AI` marks lines checked automatically by AI; people confirm or correct them.
5. Expand one invoice at a time in `Invoice accordion` to check its lines. *(PDR proposal — confirm)*

## AI checklist

- [ ] Mapping table follows Data Grids rules
- [ ] Status colours from Status tags
- [ ] AI-checked lines clearly marked

## Open questions for the team — cleanup

- **Overlap with archived components:** `Invoice delivery status` and `Invoice check status` duplicate the archived `Delivery status` / `Check status`. Is this the version to keep?
- **Default properties:** `Selected cell` and `Invoice tooltip` still use “Property 1”; `Invoice delivery status` uses colour names as State values (Yellow, Green). Rename to meanings (e.g. Status: Open, Checked).
- **Language:** `Invoice status · Nicht geprüft` — apply the language rule (English values, German labels).
- **Single-variant sets:** `Invoice price chip`, `Invoice status` and the mapping table have only one variant. Add the missing states or values.
- **Deprecated layers:** `Delivery note mapping table with toolbar` still contains `Deprecated/…` layers.
- **Unused:** `Receipt PDF`, `Repair cost approval (RKÜ)` and `Invoice accordion` have no uses in this file.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Wrapper | Built from |
|---|---|---|
| Invoice accordion | `<pdr-invoice-accordion>` | `mat-expansion-panel` (see `../md3/expansion-panel.md`) |
| Invoice status / check / delivery status | `pdr-check-status`, `pdr-delivery-status` | see `status-tags.md` (Check status / Delivery status) — same component, invoice context |
| Invoice arrows | `<pdr-status-arrow status="success|warning|error">` | icon in `--pdr-sys-success` / `--pdr-sys-warning` / `--mat-sys-error` |
| Invoice price chip | `pdr-price-chip` | see `status-tags.md` |
| Invoice tooltip | `pdr-rich-tooltip` | see `../md3/tooltips.md` |
| Delivery note mapping table | `mat-table` + `pdr-toolbar` | Selected cell → `pdr-cell--selected` (primary-container) |
| Receipt PDF | `<pdr-pdf-viewer>` | embedded viewer in `pdr-panel` |
| Repair cost approval (RKÜ) | `<pdr-rku-form>` | form fields + `mat-table` |

Amounts: `CurrencyPipe` with `'EUR'` and `de-DE`, `font-variant-numeric: tabular-nums`, right-aligned.
