# Grids & Breakpoints

Figma page: **Grids and Breakpoints 🟢** `3384:546` · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3384-546)
Source: grid styles `PDR Grids/*`, section "PDR Layout grids" `4452:46926`, collection `Breakpoints`.

## Breakpoints (current — Bootstrap-aligned)

The product uses Bootstrap-style breakpoints (Figma: "Current (bootstrap) breakpoints"). MD3 default window classes are listed only for reference — **do not use them for layout**, except where a spec says so explicitly (Data grid mobile switch at `Breakpoints.Handset`, < 600 px).

| Token | Range | Device (Figma) | MD3 window class (reference) |
|---|---|---|---|
| `XS` | 0 – 575 px | Mobile portrait | compact (0–599) |
| `S` | 576 – 767 px | Mobile landscape | compact / medium (600–839) |
| `M` | 768 – 991 px | Tablet portrait | medium |
| `L` | 992 – 1199 px | Tablet landscape | expanded (840–1199) |
| `XL` | 1200 – 1599 px | Laptop | large (1200–1599) |
| `XXL` | ≥ 1600 px | Desktop | extra-large (1600+) |

```ts
// libs/ui/src/lib/layout/breakpoints.ts — single source; never hard-code media queries elsewhere
export const PDR_BREAKPOINTS = {
  xs: '(max-width: 575.98px)',
  s:  '(min-width: 576px) and (max-width: 767.98px)',
  m:  '(min-width: 768px) and (max-width: 991.98px)',
  l:  '(min-width: 992px) and (max-width: 1199.98px)',
  xl: '(min-width: 1200px) and (max-width: 1599.98px)',
  xxl:'(min-width: 1600px)',
  mobile:  '(max-width: 767.98px)',   // XS + S
  tablet:  '(min-width: 768px) and (max-width: 1199.98px)', // M + L
  desktop: '(min-width: 1200px)',    // XL + XXL
} as const;
```
Use with `BreakpointObserver.observe(PDR_BREAKPOINTS.mobile)`. SCSS mirror:
```scss
$pdr-breakpoints: (s: 576px, m: 768px, l: 992px, xl: 1200px, xxl: 1600px);
@mixin pdr-up($bp) { @media (min-width: map.get($pdr-breakpoints, $bp)) { @content; } }
```

## Column grid (layout regions OFF)

| BP | Columns | Gutter | Margin | Column width | Content width |
|---|---|---|---|---|---|
| XS | 4 | 16 | 16 (`--pdr-space-16`) | stretch | fluid |
| S | 4 | 16 | 16 | stretch | fluid |
| M | 8 | 16 | 32 (`--pdr-space-32`) | stretch | fluid |
| L | 12 | 24 | 24 (`--pdr-space-24`) | stretch | fluid |
| XL | 12 | 24 | centered | 64 | 1032 px |
| XXL | 12 | 24 | centered | 72 | **1128 px fixed** |

```scss
.pdr-page-grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: var(--pdr-space-16);
  padding-inline: var(--pdr-space-16);
  @include pdr-up(m)  { grid-template-columns: repeat(8, minmax(0, 1fr)); padding-inline: var(--pdr-space-32); }
  @include pdr-up(l)  { grid-template-columns: repeat(12, minmax(0, 1fr)); gap: var(--pdr-space-24); padding-inline: var(--pdr-space-24); }
  @include pdr-up(xl) { max-width: 1032px; margin-inline: auto; padding-inline: 0; }
  @include pdr-up(xxl){ max-width: 1128px; }
}
```
Page examples (`../examples/*`) use a simpler rule that matches the examples: content container padding 24 px (≥ M) / 16 px (< M), panels up to **1128 px** wide.

## Layout regions (regions ON)

| BP | Top app bar | Navigation | Bottom |
|---|---|---|---|
| XS / S | 56 px | drawer (`mode="over"`) | 56 px bottom bar region |
| M | 56 px | nav rail 72 px | — |
| L / XL | 64 px | nav rail 80 px | — |
| XXL | 64 px | rail / expanded drawer | — |

The 2026 App bar (`../components/pdr/appbar-page-header.md`) is 64 px on all sizes in the examples; follow the examples when they differ from the generic regions.

## Widget grid (dashboards)

"Grid v2 (ngx-widget-grid)": start-page dashboards use **ngx-widget-grid**. Building blocks `Layout grid/1–5 columns` (`4540:16232`, `4540:15894`, `4540:15890`, `4540:15886`, `5399:43547`) define the column layouts available for widgets (`pdr-widget`, see `../components/pdr/panels-widgets.md`). Gutters: 24 px (desktop/tablet), 16 px (mobile).

## Rules
- Never hard-code pixel media queries in components — import `PDR_BREAKPOINTS` / `pdr-up()`.
- Margins and gutters only from the spacing scale (16 / 24 / 32).
- Test every page at 375, 768, 992, 1200 and 1600 px.
