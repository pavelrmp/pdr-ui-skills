# Theming rules — Angular Material M3

Token values and usage per category: `tokens/` (colors, typography, spacing, shape, elevation, state layers, motion).

Load order in `styles.scss`: `_pdr-theme.scss` → `_pdr-overrides.scss` → app styles.

## 1. Principles

- Figma's `mat` collection uses a **custom tonal mapping**, not a generated M3 palette. For example, the light primary container is blue/95, where M3 would use 90. **Never regenerate palettes** from a seed color. Override each `--mat-sys-*` role explicitly.
- Every color is a single `light-dark(LIGHT, DARK)` value; the scheme is switched with `color-scheme`.
- Typescale, shape scale and state-layer opacities in Figma equal M3 defaults, so they are **not overridden**. Only the bold weight (600) differs.
- Component customizations go through `mat.<component>-overrides()` scoped to `html` (global) or a `.pdr-*` modifier class. Every override must cite the Figma divergence in a comment.
- Global density stays 0. Figma heights (fields 56, menu/list items 48, buttons 40) match it.

## 2. `_pdr-theme.scss`

```scss
@use '@angular/material' as mat;

html {
  color-scheme: light;
  @include mat.theme((
    color: (theme-type: color-scheme, primary: mat.$azure-palette), // placeholder — fully overridden below
    typography: (plain-family: Roboto, brand-family: Roboto,
                 regular-weight: 400, medium-weight: 500, bold-weight: 600), // Figma Weight/Bold = Roboto SemiBold
    density: 0,
  ));

  // Figma collection 'mat' (modes Light / Dark)
  @include mat.theme-overrides((
      primary: light-dark(#1f65d6, #62b7f8),
      on-primary: light-dark(#ffffff, #182c53),
      primary-container: light-dark(#dbeefe, #182c53),
      on-primary-container: light-dark(#1f4889, #c0e2fd),
      inverse-primary: light-dark(#94d2fc, #1f65d6),
      secondary: light-dark(#20b6d2, #20b6d2),
      on-secondary: light-dark(#ffffff, #0b3343),
      secondary-container: light-dark(#d4f6f9, #194f62),
      on-secondary-container: light-dark(#194f62, #a8f3fb),
      tertiary: light-dark(#a5e446, #a5e446),
      on-tertiary: light-dark(#1b2e08, #1b2e08),
      tertiary-container: light-dark(#daf8a2, #375219),
      on-tertiary-container: light-dark(#375219, #daf8a2),
      error: light-dark(#d32f2f, #f17878),
      on-error: light-dark(#ffffff, #420d0d),
      error-container: light-dark(#fde3e3, #420d0d),
      on-error-container: light-dark(#7d000c, #fbcdcd),
      surface: light-dark(#f8fafc, #020616),
      on-surface: light-dark(#020616, #f8fafc),
      surface-variant: light-dark(#ffffff, #0f172a),
      on-surface-variant: light-dark(#344254, #ccd5e1),
      surface-dim: light-dark(#e2e8f0, #020616),
      surface-container-lowest: light-dark(#ffffff, #0f172a),
      surface-container-low: light-dark(#f8fafc, #1e293b),
      surface-container: light-dark(#f1f5f9, #344254),
      surface-container-high: light-dark(#e2e8f0, #485668),
      surface-container-highest: light-dark(#ccd5e1, #65758a),
      inverse-surface: light-dark(#020616, #e2e8f0),
      inverse-on-surface: light-dark(#f1f5f9, #020616),
      outline: light-dark(#65758a, #65758a),
      outline-variant: light-dark(#ccd5e1, #344254),
      shadow: light-dark(#020616, #000000),
      surface-bright: light-dark(#f8fafc, #1e293b),
      surface-tint: light-dark(#1f65d6, #62b7f8),
      scrim: light-dark(#000000, #000000),
      corner-none: 0, corner-extra-small: 4px, corner-small: 8px, corner-medium: 12px,
      corner-large: 16px, corner-extra-large: 28px, corner-full: 9999px, // Figma Full = 1000
  ));
}
html.pdr-dark { color-scheme: dark; }

// Elevation — effect styles M3/Elevation Light|Dark/1–5.
// Shadow lists contain commas, so they live outside the Sass map.
html {
  --pdr-shadow-rgb: 2 6 22; // sys/shadow Light #020616
  --mat-sys-level0: none;
  --mat-sys-level1: 0 1px 2px 0 rgb(var(--pdr-shadow-rgb) / .30), 0 1px 3px 1px rgb(var(--pdr-shadow-rgb) / .15);
  --mat-sys-level2: 0 1px 2px 0 rgb(var(--pdr-shadow-rgb) / .30), 0 2px 6px 2px rgb(var(--pdr-shadow-rgb) / .15);
  --mat-sys-level3: 0 1px 3px 0 rgb(var(--pdr-shadow-rgb) / .30), 0 4px 8px 3px rgb(var(--pdr-shadow-rgb) / .15);
  --mat-sys-level4: 0 2px 3px 0 rgb(var(--pdr-shadow-rgb) / .30), 0 6px 10px 4px rgb(var(--pdr-shadow-rgb) / .15);
  --mat-sys-level5: 0 4px 4px 0 rgb(var(--pdr-shadow-rgb) / .30), 0 8px 12px 6px rgb(var(--pdr-shadow-rgb) / .15);
}
html.pdr-dark { --pdr-shadow-rgb: 0 0 0; } // sys/shadow Dark #000000
```

## 3. PDR-only custom properties (`--pdr-*`)

Not part of M3. Prefer generating them from `tokens.json` with Style Dictionary (`sys.color-extended`, `ref.spacing`, `ref.dialog-width`); hand-written equivalent:

```scss
html {
  --pdr-sys-on-surface-disabled: light-dark(#95a4b7, #65758a);
  --pdr-sys-on-surface-link: light-dark(#1f65d6, #62b7f8);
  --pdr-sys-success: light-dark(#327c36, #6bbd6f);
  --pdr-sys-on-success: light-dark(#ffffff, #0e2511);
  --pdr-sys-success-container: light-dark(#e3f5e3, #0e2511);
  --pdr-sys-on-success-container: light-dark(#224525, #c8eac9);
  --pdr-sys-info: light-dark(#1f65d6, #62b7f8);
  --pdr-sys-on-info: light-dark(#ffffff, #182c53);
  --pdr-sys-info-container: light-dark(#dbeefe, #182c53);
  --pdr-sys-on-info-container: light-dark(#1f4889, #c0e2fd);
  --pdr-sys-warning: light-dark(#cb9303, #ebbe07);
  --pdr-sys-on-warning: light-dark(#ffffff, #422306);
  --pdr-sys-warning-container: light-dark(#fefcc3, #422306);
  --pdr-sys-on-warning-container: light-dark(#714312, #fff589);
  --pdr-sys-orange: light-dark(#de5518, #ed6c1f);
  --pdr-sys-on-orange: light-dark(#ffffff, #40140a);
  --pdr-sys-orange-container: light-dark(#fdecd7, #40140a);
  --pdr-sys-on-orange-container: light-dark(#772d17, #fad4ae);
  --pdr-sys-amber: light-dark(#d37709, #f09e0f);
  --pdr-sys-on-amber: light-dark(#ffffff, #401c07);
  --pdr-sys-amber-container: light-dark(#fcf3cb, #401c07);
  --pdr-sys-on-amber-container: light-dark(#723715, #fae792);
  --pdr-sys-lime: light-dark(#67a221, #86ca2e);
  --pdr-sys-on-lime: light-dark(#ffffff, #1b2e08);
  --pdr-sys-lime-container: light-dark(#edfbcd, #1b2e08);
  --pdr-sys-on-lime-container: light-dark(#375219, #daf8a2);
  --pdr-sys-emerald: light-dark(#35966a, #44b982);
  --pdr-sys-on-emerald: light-dark(#ffffff, #0e2b22);
  --pdr-sys-emerald-container: light-dark(#d8f9e6, #0e2b22);
  --pdr-sys-on-emerald-container: light-dark(#1e4d3c, #b6f2d2);
  --pdr-sys-teal: light-dark(#359489, #44b8a7);
  --pdr-sys-on-teal: light-dark(#ffffff, #112e2e);
  --pdr-sys-teal-container: light-dark(#d5faf1, #112e2e);
  --pdr-sys-on-teal-container: light-dark(#234d4a, #acf4e4);
  --pdr-sys-pink: light-dark(#e72565, #fc6aa5);
  --pdr-sys-on-pink: light-dark(#ffffff, #54031a);
  --pdr-sys-pink-container: light-dark(#fde6f0, #54031a);
  --pdr-sys-on-pink-container: light-dark(#8a1134, #fecce2);
  --pdr-sys-purple: light-dark(#aa38c1, #d886ec);
  --pdr-sys-on-purple: light-dark(#ffffff, #3f0c46);
  --pdr-sys-purple-container: light-dark(#f8eafd, #3f0c46);
  --pdr-sys-on-purple-container: light-dark(#64236c, #f0d5f9);
  --pdr-sys-cyan: light-dark(#1c7993, #33d3ec);
  --pdr-sys-on-cyan: light-dark(#ffffff, #0b3343);
  --pdr-sys-cyan-container: light-dark(#d4f6f9, #0b3343);
  --pdr-sys-on-cyan-container: light-dark(#194f62, #a8f3fb);
  --pdr-sys-indigo: light-dark(#4c3aed, #7e86fb);
  --pdr-sys-on-indigo: light-dark(#ffffff, #1d1a4a);
  --pdr-sys-indigo-container: light-dark(#e1e7fd, #1d1a4a);
  --pdr-sys-on-indigo-container: light-dark(#302c80, #c9d2fc);

  // spacing (Figma 'space')
  --pdr-space-2: 2px;  --pdr-space-4: 4px;  --pdr-space-6: 6px;  --pdr-space-8: 8px;
  --pdr-space-12: 12px; --pdr-space-16: 16px; --pdr-space-24: 24px; --pdr-space-32: 32px;
  --pdr-space-40: 40px; --pdr-space-48: 48px; --pdr-space-56: 56px; --pdr-space-64: 64px;
  --pdr-space-72: 72px; --pdr-space-80: 80px; --pdr-space-88: 88px; --pdr-space-96: 96px;

  // dialog widths (Figma 'Modals')
  --pdr-dialog-width-s: 280px; --pdr-dialog-width-m: 420px; --pdr-dialog-width-l: 560px;
  --pdr-dialog-width-xl: 900px; --pdr-dialog-width-xxl: 1200px; --pdr-dialog-width-xxxl: 1536px;

  // state layers (Figma state-layer/on surface/Opacity-8|12|16)
  --pdr-state-layer-on-surface-8:  color-mix(in srgb, var(--mat-sys-on-surface) 8%, transparent);
  --pdr-state-layer-on-surface-12: color-mix(in srgb, var(--mat-sys-on-surface) 12%, transparent);
  --pdr-state-layer-on-surface-16: color-mix(in srgb, var(--mat-sys-on-surface) 16%, transparent);

  // PDR-only type scales
  --pdr-sys-display-xl: 600 96px / 96px Roboto, sans-serif;   // tracking -3.84px
  --pdr-sys-label-large-prominent: 600 14px / 20px Roboto, sans-serif;
  --pdr-sys-label-medium-prominent: 600 12px / 16px Roboto, sans-serif;
}
.pdr-icon--filled { font-variation-settings: 'FILL' 1; }
```

## 4. Component overrides — where they live

Each component file in `components/md3/` and `components/pdr/` ends with an **Overrides** section. One SCSS partial per file, same name:

```
styles/
  _pdr-theme.scss
  _pdr-overrides.scss          // forwards everything below
  components/md3/_buttons.scss, _dialogs.scss, _text-fields.scss, …
  components/pdr/_alerts.scss, _status-tags.scss, …
```
```scss
// _pdr-overrides.scss
@use 'components/md3/buttons';
@use 'components/md3/cards';
@use 'components/md3/chips';
@use 'components/md3/data-grids';
@use 'components/md3/dialogs';
@use 'components/md3/divider';
@use 'components/md3/menu';
@use 'components/md3/input';
@use 'components/md3/bottom-sheet';
@use 'components/pdr/navigation-menu';
@use 'components/md3/sheets';
@use 'components/md3/form-fields';
@use 'components/md3/toolbar';
@use 'components/md3/tooltips';
@use 'components/md3/tree';
// pdr/* styles are component-scoped (styleUrl) — only global helpers go here
```

Global divergences from M3 defaults (the only ones):

| Component | Figma vs M3 default | File |
|---|---|---|
| Button (tonal) | primary-container (M3: secondary-container) | `md3/buttons.md` |
| Button padding | 16px horizontal (M3: 24px) | `md3/buttons.md` |
| FAB "Primary" | primary (M3 FAB default: primary-container) | `md3/buttons.md` |
| Dialog | surface-container-lowest + level5 (M3: surface-container-high, no shadow) | `md3/dialogs.md` |
| Nav drawer item | 56px, corner-full | `pdr/navigation-menu.md` |
| Toolbar | 88px, surface-container-lowest, corner-large | `md3/toolbar.md` |

Pages with "None — Figma matches M3 defaults" must stay override-free.

Breakpoint mixins (`pdr-up()`) and `PDR_BREAKPOINTS` are defined in `foundations/grids-breakpoints.md`.

## 5. Writing new overrides — checklist

1. Confirm the divergence in Figma (bound variable name, not eyeballing).
2. Find the token key on the component's **Styling** tab at material.angular.dev for the installed version. Token names change between majors (e.g. `elevated-*` → `protected-*` for buttons).
3. Values must be `var(--mat-sys-*)` / `var(--pdr-*)`, never literals (exception: component heights/paddings from Figma geometry).
4. Scope: `html` for global divergence, `.pdr-<component>--<modifier>` for variants.
5. If a key fails to compile, fix the key. Never fall back to `!important`, `::ng-deep` or `.mdc-*` selectors.

## 6. Known Figma data caveats

- Dark-mode state-layer variables alias a deleted variable, so Material's default state-layer opacities (.08 / .12 / .12 / .16) are used.
- `surface-bright` and `surface-tint` are not in Figma; they are derived (`pdr.derived` in tokens.json). `scrim` is in Figma (`#00000052`): the role is black, the 32 % opacity is applied by the backdrop.
- Measured contrast failures (light mode): `on-secondary`/`secondary` 2.42, `on-warning`/`warning` 2.72, `warning` on surface 2.60 — see `foundations/accessibility.md` for the full table and mandatory workarounds.
- Palette anomalies: `purple/99` = `indigo/99`; `red/99` and `cool grey/99` hold M3-baseline leftovers.
