# Typography

Figma: **⚛️ Design Tokens** page `3313:3` · [1. Typography tokens](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3338-3944) · [2. Text Styles Desktop](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3317-109)
Machine-readable source: `../../tokens.json`. Theme setup: `../theming-rules.md`.

## Typefaces

| Token | Value | Figma variable | CSS |
|---|---|---|---|
| Brand | Roboto | `Typeface/Brand` | `--mat-sys-brand-font-family` (via `mat.theme` `brand-family`) |
| Plain | Roboto | `Typeface/Plain` | `plain-family` |
| Weight regular / medium / bold | 400 / 500 / **600** | `Typescale/Weight/*` | `regular-weight` / `medium-weight` / `bold-weight` |

Figma “Weight/Bold” is **Roboto SemiBold (600)**, not 700. The Typeface collection also has a **Wireframe** mode (Flow Circular) for low-fidelity mock-ups — never use it in production.

## Rules

1. Set text only through tokens: `font: var(--mat-sys-body-medium); letter-spacing: var(--mat-sys-body-medium-tracking);` — never font-size / weight / line-height by hand.
2. Pick the style by role, not by size (table below).
3. One `<h1>` per page = the Page header title. Heading level (h2, h3) follows document structure; the visual style comes from the token.
4. Long reading text uses `body-large` (line height 1.5, WCAG). `body-medium` is for compact UI text.
5. The scale equals the M3 defaults — no overrides in the theme.

## Type scale

| Token | Figma name | Font | Weight | Size / line height | Tracking | CSS | Use in PDR |
|---|---|---|---|---|---|---|---|
| display-large | Display Large (H1) | Brand | 400 | 57px / 64px | -0.25px | `--mat-sys-display-large` | Rare — marketing / empty hero |
| display-medium | Display Medium (H2) | Brand | 400 | 45px / 52px | 0px | `--mat-sys-display-medium` | Rare — marketing |
| display-small | Display Small (H3) | Brand | 400 | 36px / 44px | 0px | `--mat-sys-display-small` | Page title (desktop/tablet) — Page header only |
| headline-large | Headline Large (H4) | Brand | 400 | 32px / 40px | 0px | `--mat-sys-headline-large` |  |
| headline-medium | Headline Medium (H5) | Brand | 400 | 28px / 36px | 0px | `--mat-sys-headline-medium` | Page title (mobile) — Page header only |
| headline-small | Headline Small (H6) | Brand | 400 | 24px / 32px | 0px | `--mat-sys-headline-small` | Modal / dialog titles |
| title-large | Title Large | Brand | 400 | 22px / 28px | 0px | `--mat-sys-title-large` | Panel titles (MD3 panel title), top app bar |
| title-medium | Title Medium (Subtitle 1) | Plain | 500 | 16px / 24px | 0.15px | `--mat-sys-title-medium` | Card headers, list emphasis, alert titles, total in table footer |
| title-small | Title Small (Subtitle 2) | Plain | 500 | 14px / 20px | 0.1px | `--mat-sys-title-small` | Tabs, table header emphasis |
| body-large | Body Large (Body 1) | Plain | 400 | 16px / 24px | 0.5px | `--mat-sys-body-large` | Inputs, list items, long reading text (≥ 1.5 line height) |
| body-medium | Body Medium (Body 2) | Plain | 400 | 14px / 20px | 0.25px | `--mat-sys-body-medium` | Default UI text, table cells, dialog text |
| body-small | Body Small (Caption, Field Label, Helper) | Plain | 400 | 12px / 16px | 0.4px | `--mat-sys-body-small` | Captions, field labels, helper / supporting text, tooltips |
| label-large | Label Large (Button) | Plain | 500 | 14px / 20px | 0.1px | `--mat-sys-label-large` | Buttons, chips, status tags |
| label-medium | Label Medium | Plain | 500 | 12px / 16px | 0.5px | `--mat-sys-label-medium` | Labels in definition lists |
| label-small | Label Small | Plain | 500 | 11px / 16px | 0.5px | `--mat-sys-label-small` | Badges |

## PDR additions

| Token | Figma | Value | CSS |
|---|---|---|---|
| display-xl | text style `PDR/dislpay xl (-4%)` | Roboto 600, 96 / 96, -3.84 px | `--pdr-sys-display-xl` |
| label-large-prominent | `Typescale/Label Large/Weight Prominent` | 600, 14 / 20, 0.1 px | `--pdr-sys-label-large-prominent` |
| label-medium-prominent | `Typescale/Label Medium/Weight Prominent` | 600, 12 / 16, 0.5 px | `--pdr-sys-label-medium-prominent` |

## Accessibility modes (Figma `Typescale` collection: 100 % / 150 % / 200 %)

The 150 % and 200 % modes show how text scales for users who enlarge text. In code this happens through browser text size / zoom — **don’t ship separate themes**. Test every page at 200 % text size (see `../foundations/accessibility.md`).

```scss
.pdr-section-title { font: var(--mat-sys-title-large); letter-spacing: var(--mat-sys-title-large-tracking); color: var(--mat-sys-on-surface); }
```
