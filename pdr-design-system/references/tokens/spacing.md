# Spacing

Figma: **⚛️ Design Tokens** page `3313:3` · [Spacing tokens](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3326-2292)
Machine-readable source: `../../tokens.json`. Theme setup: `../theming-rules.md`.

Figma collection `space` (16 values). CSS: `--pdr-space-N`.

## Scale

| Token | Value | CSS | Typical use |
|---|---|---|---|
| space-2 | 2 px | `--pdr-space-2` | Hairline gaps, status-tag vertical padding |
| space-4 | 4 px | `--pdr-space-4` | Icon ↔ text in tags, divider ↔ supporting text |
| space-6 | 6 px | `--pdr-space-6` | Rare — tight inline gaps |
| space-8 | 8 px | `--pdr-space-8` | Gap between buttons, chips, filter row items; small paddings |
| space-12 | 12 px | `--pdr-space-12` | Cell padding (vertical), gaps in compact groups |
| space-16 | 16 px | `--pdr-space-16` | Panel padding, list item padding, mobile page margin, divider insets |
| space-24 | 24 px | `--pdr-space-24` | Page margin (≥ 768 px), dialog padding, gutters (≥ 992 px), section gaps |
| space-32 | 32 px | `--pdr-space-32` | Page margin on tablet (M grid), large section gaps |
| space-40 | 40 px | `--pdr-space-40` | Large gaps |
| space-48 | 48 px | `--pdr-space-48` | Nested nav item indent, empty-state spacing |
| space-56 | 56 px | `--pdr-space-56` | Layout blocks |
| space-64 | 64 px | `--pdr-space-64` | Layout blocks |
| space-72 | 72 px | `--pdr-space-72` | Layout blocks |
| space-80 | 80 px | `--pdr-space-80` | Layout blocks |
| space-88 | 88 px | `--pdr-space-88` | Layout blocks |
| space-96 | 96 px | `--pdr-space-96` | Hero / empty-state spacing |

## Rules

1. Every padding, margin and gap comes from this scale. Off-scale values are a bug.
2. Prefer flex/grid `gap` over margins between siblings.
3. Component-internal spacing (button padding, field height) comes from Material — don’t add spacing inside Material components.
4. Page layout (margins, gutters, columns per breakpoint) is defined in `../foundations/grids-breakpoints.md`.

## Related size tokens

| Collection | Values | Where |
|---|---|---|
| `Modals` | S 280 · M 420 · L 560 · XL 900 · XXL 1200 · XXXL 1536 (`--pdr-dialog-width-*`) | `../components/md3/dialogs.md` |
| `Breakpoints` | XS 375 · S 576 · M 768 · L 992 · XL 1200 · XXL 1600 | `../foundations/grids-breakpoints.md` |
| Content width | 1128 px max | `../foundations/grids-breakpoints.md` |
