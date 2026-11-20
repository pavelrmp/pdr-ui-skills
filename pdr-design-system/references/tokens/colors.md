# Colors

Figma: **⚛️ Design Tokens** page `3313:3` · [MD3 UI Color scheme](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=4592-21250) · [ref color tokens](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3321-188) · [Palette](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=5656-24871) · [Brand](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=5663-21691)
Machine-readable source: `../../tokens.json`. Theme setup: `../theming-rules.md`.

## Rules

1. **Use roles, never palette tones.** Components use `var(--mat-sys-*)` (M3 roles) or `var(--pdr-sys-*)` (PDR roles). The `ref` palette below exists only to build the roles — never reference `blue/40` or a hex value in component code.
2. **Pair colors correctly.** Text and icons on a colored background use the matching *on* role: `on-primary` on `primary`, `on-X-container` on `X-container`.
3. **Light and dark are automatic.** Every role is one `light-dark()` value; switch with `color-scheme` (see `../theming-rules.md`). Never write separate dark-mode colors.
4. **PDR mapping is custom, not M3-generated.** Containers use tone 95 (not 90) and *on-containers* tone 25 (not 10). Don’t regenerate palettes from a seed color.
5. **Contrast:** `on-secondary`/`secondary`, `on-warning`/`warning` and `warning` on surface fail WCAG in light mode — use the `-container` roles for text. Full table: `../foundations/accessibility.md`.

## Where each surface is used (Figma labels)

| Role | Figma label | Use |
|---|---|---|
| `surface` | Surface (Page BG) | Page background |
| `surface-container-lowest` | Surf. Container Lowest (Panel) | Panels, dialogs, app bar content areas |
| `surface-container-low` | Surf. Container Low | Elevated cards, bottom sheets |
| `surface-container` | Surf. Container | Menus, autocomplete panel, rich tooltip |
| `surface-container-high` / `-highest` | Surf. Container High / Highest | Skeletons, filled cards, neutral tags |
| `surface-variant` | — | Side sheets |
| `outline` | Outline | Text-field borders (≥ 3:1) |
| `outline-variant` | Outline Variant | Dividers, outlined cards, table header divider — decorative only |
| `on-surface-variant` | On Surface Var. | Secondary text, icons in icon buttons |
| `on-surface-disabled` | On Surface Disabled | Disabled text (PDR role) |
| `on-surface-link` | — | Links (PDR role) |
| `scrim` | Skrim (N-0) | Modal backdrops: black, applied at **32 % opacity** by the backdrop (Figma `#00000052`) |

## Brand

| Role | CSS variable | Figma variable | Light | Dark |
|---|---|---|---|---|
| primary | `--mat-sys-primary` | `mat/sys/brand/primary/primary` | blue/40 `#1f65d6` | blue/70 `#62b7f8` |
| on-primary | `--mat-sys-on-primary` | `mat/sys/brand/primary/on primary` | blue/100 `#ffffff` | blue/20 `#182c53` |
| primary-container | `--mat-sys-primary-container` | `mat/sys/brand/primary/primary container` | blue/95 `#dbeefe` | blue/20 `#182c53` |
| on-primary-container | `--mat-sys-on-primary-container` | `mat/sys/brand/primary/on primary container` | blue/25 `#1f4889` | blue/90 `#c0e2fd` |
| inverse-primary | `--mat-sys-inverse-primary` | `mat/sys/surface/inverse primary` | blue/80 `#94d2fc` | blue/40 `#1f65d6` |
| secondary | `--mat-sys-secondary` | `mat/sys/brand/secondary/secondary` | cyan/60 `#20b6d2` | cyan/60 `#20b6d2` |
| on-secondary | `--mat-sys-on-secondary` | `mat/sys/brand/secondary/on secondary` | cyan/100 `#ffffff` | cyan/20 `#0b3343` |
| secondary-container | `--mat-sys-secondary-container` | `mat/sys/brand/secondary/secondary container` | cyan/95 `#d4f6f9` | cyan/25 `#194f62` |
| on-secondary-container | `--mat-sys-on-secondary-container` | `mat/sys/brand/secondary/on secondary container` | cyan/25 `#194f62` | cyan/90 `#a8f3fb` |
| tertiary | `--mat-sys-tertiary` | `mat/sys/brand/tertiary/tertiary` | lime/70 `#a5e446` | lime/70 `#a5e446` |
| on-tertiary | `--mat-sys-on-tertiary` | `mat/sys/brand/tertiary/on tertiary` | lime/20 `#1b2e08` | lime/20 `#1b2e08` |
| tertiary-container | `--mat-sys-tertiary-container` | `mat/sys/brand/tertiary/tertiary container` | lime/90 `#daf8a2` | lime/25 `#375219` |
| on-tertiary-container | `--mat-sys-on-tertiary-container` | `mat/sys/brand/tertiary/on tertiary container` | lime/25 `#375219` | lime/90 `#daf8a2` |

## Error

| Role | CSS variable | Figma variable | Light | Dark |
|---|---|---|---|---|
| error | `--mat-sys-error` | `mat/sys/semantic/error/error` | red/50 `#d32f2f` | red/70 `#f17878` |
| on-error | `--mat-sys-on-error` | `mat/sys/semantic/error/on error` | red/100 `#ffffff` | red/20 `#420d0d` |
| error-container | `--mat-sys-error-container` | `mat/sys/semantic/error/error container` | red/95 `#fde3e3` | red/20 `#420d0d` |
| on-error-container | `--mat-sys-on-error-container` | `mat/sys/semantic/error/on error container` | red/25 `#7d000c` | red/90 `#fbcdcd` |

## Surfaces

| Role | CSS variable | Figma variable | Light | Dark |
|---|---|---|---|---|
| surface | `--mat-sys-surface` | `mat/sys/surface/surface` | cool grey/98 `#f8fafc` | cool grey/20 `#020616` |
| on-surface | `--mat-sys-on-surface` | `mat/sys/surface/on surface` | cool grey/20 `#020616` | cool grey/98 `#f8fafc` |
| surface-variant | `--mat-sys-surface-variant` | `mat/sys/surface/surface variant` | cool grey/100 `#ffffff` | cool grey/25 `#0f172a` |
| on-surface-variant | `--mat-sys-on-surface-variant` | `mat/sys/surface/on surface variant` | cool grey/40 `#344254` | cool grey/80 `#ccd5e1` |
| surface-dim | `--mat-sys-surface-dim` | `mat/sys/surface/surface dim` | cool grey/90 `#e2e8f0` | cool grey/20 `#020616` |
| surface-bright | `--mat-sys-surface-bright` | `*derived*` | cool grey/98 `#f8fafc` | cool grey/30 `#1e293b` |
| surface-container-lowest | `--mat-sys-surface-container-lowest` | `mat/sys/surface container/surface container lowest` | cool grey/100 `#ffffff` | cool grey/25 `#0f172a` |
| surface-container-low | `--mat-sys-surface-container-low` | `mat/sys/surface container/surface container low` | cool grey/98 `#f8fafc` | cool grey/30 `#1e293b` |
| surface-container | `--mat-sys-surface-container` | `mat/sys/surface container/surface container` | cool grey/95 `#f1f5f9` | cool grey/40 `#344254` |
| surface-container-high | `--mat-sys-surface-container-high` | `mat/sys/surface container/surface container high` | cool grey/90 `#e2e8f0` | cool grey/50 `#485668` |
| surface-container-highest | `--mat-sys-surface-container-highest` | `mat/sys/surface container/surface container highest` | cool grey/80 `#ccd5e1` | cool grey/60 `#65758a` |
| inverse-surface | `--mat-sys-inverse-surface` | `mat/sys/surface/inverse surface` | cool grey/20 `#020616` | cool grey/90 `#e2e8f0` |
| inverse-on-surface | `--mat-sys-inverse-on-surface` | `mat/sys/surface/inverse on surface` | cool grey/95 `#f1f5f9` | cool grey/20 `#020616` |
| on-surface-disabled | `--pdr-sys-on-surface-disabled` | `mat/sys/surface/on surface disabled` | cool grey/70 `#95a4b7` | cool grey/60 `#65758a` |
| on-surface-link | `--pdr-sys-on-surface-link` | `mat/sys/surface/on surface link` | blue/40 `#1f65d6` | blue/70 `#62b7f8` |

## Outlines, shadow, scrim

| Role | CSS variable | Figma variable | Light | Dark |
|---|---|---|---|---|
| outline | `--mat-sys-outline` | `mat/sys/outlines/outline` | cool grey/60 `#65758a` | cool grey/60 `#65758a` |
| outline-variant | `--mat-sys-outline-variant` | `mat/sys/outlines/outline variant` | cool grey/80 `#ccd5e1` | cool grey/40 `#344254` |
| shadow | `--mat-sys-shadow` | `mat/sys/shadow` | — `#020616` | — `#000000` |
| scrim | `--mat-sys-scrim` | `mat/sys/scrim` | — `#000000` (backdrop at 32 %) | — `#000000` (backdrop at 32 %) |
| surface-tint | `--mat-sys-surface-tint` | `*derived*` | blue/40 `#1f65d6` | blue/70 `#62b7f8` |

Secondary = **Cyan**, Tertiary = **Lime** (Figma labels “Secondary (Cyan)”, “Tertiary (Lime)”). `surface-bright` and `surface-tint` are not in Figma; they are derived (`pdr.derived` in tokens.json).

## Semantic colors (PDR roles)

Used for alerts, status tags and feedback. Same four-role pattern as M3: `X`, `on-X`, `X-container`, `on-X-container`.

| Role | CSS variable | Light | Dark |
|---|---|---|---|
| success | `--pdr-sys-success` | green/50 `#327c36` | green/70 `#6bbd6f` |
| on-success | `--pdr-sys-on-success` | green/100 `#ffffff` | green/20 `#0e2511` |
| success-container | `--pdr-sys-success-container` | green/95 `#e3f5e3` | green/20 `#0e2511` |
| on-success-container | `--pdr-sys-on-success-container` | green/25 `#224525` | green/90 `#c8eac9` |
| info | `--pdr-sys-info` | blue/40 `#1f65d6` | blue/70 `#62b7f8` |
| on-info | `--pdr-sys-on-info` | blue/100 `#ffffff` | blue/20 `#182c53` |
| info-container | `--pdr-sys-info-container` | blue/95 `#dbeefe` | blue/20 `#182c53` |
| on-info-container | `--pdr-sys-on-info-container` | blue/25 `#1f4889` | blue/90 `#c0e2fd` |
| warning | `--pdr-sys-warning` | yellow/50 `#cb9303` | yellow/60 `#ebbe07` |
| on-warning | `--pdr-sys-on-warning` | yellow/100 `#ffffff` | yellow/20 `#422306` |
| warning-container | `--pdr-sys-warning-container` | yellow/95 `#fefcc3` | yellow/20 `#422306` |
| on-warning-container | `--pdr-sys-on-warning-container` | yellow/25 `#714312` | yellow/90 `#fff589` |

Error uses the M3 `error` roles above. `info` uses the same tones as `primary`.

## Additional colors (PDR roles)

For categories and domain statuses only (status tags, avatars, charts) — never for UI chrome. Each color has `X`, `on-X`, `X-container`, `on-X-container`.

| Color | `X` light / dark | `X-container` light / dark | CSS prefix |
|---|---|---|---|
| orange | orange/50 `#de5518` / orange/60 `#ed6c1f` | orange/95 `#fdecd7` / orange/20 `#40140a` | `--pdr-sys-orange-*` |
| amber | amber/50 `#d37709` / amber/60 `#f09e0f` | amber/95 `#fcf3cb` / amber/20 `#401c07` | `--pdr-sys-amber-*` |
| lime | lime/50 `#67a221` / lime/60 `#86ca2e` | lime/95 `#edfbcd` / lime/20 `#1b2e08` | `--pdr-sys-lime-*` |
| emerald | emerald/50 `#35966a` / emerald/60 `#44b982` | emerald/95 `#d8f9e6` / emerald/20 `#0e2b22` | `--pdr-sys-emerald-*` |
| teal | teal/50 `#359489` / teal/60 `#44b8a7` | teal/95 `#d5faf1` / teal/20 `#112e2e` | `--pdr-sys-teal-*` |
| cyan | cyan/40 `#1c7993` / cyan/70 `#33d3ec` | cyan/95 `#d4f6f9` / cyan/20 `#0b3343` | `--pdr-sys-cyan-*` |
| indigo | indigo/50 `#4c3aed` / indigo/70 `#7e86fb` | indigo/95 `#e1e7fd` / indigo/20 `#1d1a4a` | `--pdr-sys-indigo-*` |
| pink | pink/50 `#e72565` / pink/70 `#fc6aa5` | pink/95 `#fde6f0` / pink/20 `#54031a` | `--pdr-sys-pink-*` |
| purple | purple/50 `#aa38c1` / purple/70 `#d886ec` | purple/95 `#f8eafd` / purple/20 `#3f0c46` | `--pdr-sys-purple-*` |

Fixed mappings (which status uses which color) are defined in `../components/pdr/status-tags.md`.

## Reference palette (`ref` collection)

Tonal palettes the roles are built from. **Never use these directly in components.**

| Family | 0 | 10 | 20 | 25 | 30 | 35 | 40 | 50 | 60 | 70 | 80 | 90 | 95 | 98 | 99 | 100 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| blue | `#000000` | `#0c162a` | `#182c53` | `#1f4889` | `#1f52ae` | `#1f5cc2` | `#1f65d6` | `#1d75e8` | `#3d98f4` | `#62b7f8` | `#94d2fc` | `#c0e2fd` | `#dbeefe` | `#eff8ff` | `#f7fbff` | `#ffffff` |
| red | `#000000` | `#210707` | `#420d0d` | `#7d000c` | `#930010` | `#a80616` | `#b12424` | `#d32f2f` | `#e74c4c` | `#f17878` | `#f8a9a9` | `#fbcdcd` | `#fde3e3` | `#fdf3f3` | `#fffbff` | `#ffffff` |
| orange | `#000000` | `#200a05` | `#40140a` | `#772d17` | `#933419` | `#a63a17` | `#b93f15` | `#de5518` | `#ed6c1f` | `#f18d46` | `#f6b67b` | `#fad4ae` | `#fdecd7` | `#fef6ee` | `#fffbf7` | `#ffffff` |
| amber | `#000000` | `#200e04` | `#401c07` | `#723715` | `#8c4113` | `#9d4b10` | `#ad540d` | `#d37709` | `#f09e0f` | `#f5bc1e` | `#f8d455` | `#fae792` | `#fcf3cb` | `#fefbec` | `#fffdf5` | `#ffffff` |
| green | `#000000` | `#071309` | `#0e2511` | `#224525` | `#27542a` | `#2a5e2d` | `#2d6830` | `#327c36` | `#46a14b` | `#6bbd6f` | `#9dd89f` | `#c8eac9` | `#e3f5e3` | `#f3faf3` | `#fcfefc` | `#ffffff` |
| yellow | `#000000` | `#211203` | `#422306` | `#714312` | `#86530d` | `#945e0a` | `#a26906` | `#cb9303` | `#ebbe07` | `#fbd814` | `#feea4e` | `#fff589` | `#fefcc3` | `#fefde8` | `#fffef3` | `#ffffff` |
| lime | `#000000` | `#111f00` | `#1b2e08` | `#375219` | `#3b5c00` | `#406119` | `#4f7b1b` | `#67a221` | `#86ca2e` | `#a5e446` | `#bff06d` | `#daf8a2` | `#edfbcd` | `#f7fee8` | `#fbfff3` | `#ffffff` |
| emerald | `#000000` | `#071611` | `#0e2b22` | `#1e4d3c` | `#235f47` | `#276c50` | `#2a7858` | `#35966a` | `#44b982` | `#55d197` | `#86e6b8` | `#b6f2d2` | `#d8f9e6` | `#effcf5` | `#f7fdfa` | `#ffffff` |
| teal | `#000000` | `#091717` | `#112e2e` | `#234d4a` | `#255e59` | `#296a64` | `#2c766f` | `#359489` | `#44b8a7` | `#52d2be` | `#7ce9d5` | `#acf4e4` | `#d5faf1` | `#f3fdfa` | `#f9fefd` | `#ffffff` |
| cyan | `#000000` | `#061a22` | `#0b3343` | `#194f62` | `#1a5f74` | `#1b6b82` | `#1c7993` | `#1a92b1` | `#20b6d2` | `#33d3ec` | `#6de8f8` | `#a8f3fb` | `#d4f6f9` | `#eefcfd` | `#f7fdfe` | `#ffffff` |
| indigo | `#000000` | `#0f0d25` | `#1d1a4a` | `#302c80` | `#352aa5` | `#3b2cba` | `#402ecf` | `#4c3aed` | `#615ff8` | `#7e86fb` | `#a6b3fd` | `#c9d2fc` | `#e1e7fd` | `#eff2fe` | `#f7f9ff` | `#ffffff` |
| pink | `#000000` | `#2a020d` | `#54031a` | `#8a1134` | `#a50f3a` | `#b70f40` | `#c80e46` | `#e72565` | `#f63e84` | `#fc6aa5` | `#fea3ca` | `#fecce2` | `#fde6f0` | `#fef1f7` | `#fff8fb` | `#ffffff` |
| purple | `#000000` | `#200623` | `#3f0c46` | `#64236c` | `#762583` | `#882a99` | `#9b2fae` | `#aa38c1` | `#c457de` | `#d886ec` | `#e6b3f4` | `#f0d5f9` | `#f8eafd` | `#fbf5fe` | `#f7f9ff` | `#ffffff` |
| cool grey | `#000000` | `#01030b` | `#020616` | `#0f172a` | `#1e293b` | `#293648` | `#344254` | `#485668` | `#65758a` | `#95a4b7` | `#ccd5e1` | `#e2e8f0` | `#f1f5f9` | `#f8fafc` | `#fefbff` | `#ffffff` |

Known data issues: `purple/99` equals `indigo/99`; `red/99` and `cool grey/99` hold M3-baseline leftovers.
