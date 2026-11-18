---
name: pdr-design-system
description: PDR.cloud Design System for Angular Material M3 — guardrails, Figma-to-Angular component mapping, design tokens and theming rules. Use this skill whenever implementing, reviewing or refactoring any PDR.cloud Angular UI, translating a PDR Figma frame or link (file 3N1iHNzVKurYAwq0LWsVpQ) into code, styling or theming any mat-* component, or adding colors, spacing, typography, radii or shadows — even if the user only says "build this screen", "make it match Figma", or names a PDR component (status tag, alert, panel, order card, side nav).
---

# PDR.cloud Design System → Angular Material M3

Target: **Angular Material ≥ 20** (`matButton="tonal"`, `mat.theme()`, `mat.*-overrides()`).
Figma: `PDR.cloud-Design-System` (`3N1iHNzVKurYAwq0LWsVpQ`).

## Router — load only what the task needs

Component docs mirror the Figma file: one file per Figma page, split into the two Figma sections.

| Task | Read |
|---|---|
| Any color / type / spacing / radius / shadow value | `tokens.json` (look up by `$extensions["pdr.figma"]` = Figma variable name) |
| Theme setup, dark mode, `*-overrides()` rules, CSS custom properties | `references/theming-rules.md` |
| Figma page under **↓ ANGULAR MD3 COMPONENTS** | `references/components/md3/<page>.md` |
| Figma page under **↓ PDR COMPONENTS** | `references/components/pdr/<page>.md` |
| Page layout, breakpoints, column grid, responsive behavior | `references/foundations/grids-breakpoints.md` |
| Accessibility requirements, contrast, keyboard, ARIA, testing (definition of done) | `references/foundations/accessibility.md` |
| Any icon (Material Symbols or custom PDR domain icons) | `references/foundations/icons.md` (PDR icons: Figma link + node IDs) |
| Building a whole new page / screen / modal / sheet | `references/examples/README.md` → the matching example |

**New screen?** Start from the closest example (`references/examples/`), then fill it with components.

Every component file lists the Figma node IDs, variant props → Angular mapping, and its own overrides SCSS (`styles/components/{md3,pdr}/_<page>.scss`). Open only the files for the components on the frame you are building; follow cross-links (`../pdr/…`) only when needed.

## Guardrails (non-negotiable)

1. **Material first.** A Figma frame from "↓ ANGULAR MD3 COMPONENTS" MUST be a `mat-*` component/directive. Never rebuild buttons, fields, menus, chips or dialogs from `div`s.
2. **No raw values** in component styles: no hex/rgb, px font sizes or box-shadows. Use `var(--mat-sys-*)` (M3 roles), `var(--pdr-sys-*)` (PDR-only roles), `var(--pdr-space-*)`.
3. **No `!important`, no `::ng-deep`, no `.mdc-*` / `.mat-mdc-*` selectors.** Customize only through `mat.<component>-overrides()` or documented `--mat-<component>-*` properties, scoped to a class. (Single exception: the global `prefers-reduced-motion` rule in `references/foundations/accessibility.md`.)
4. **Typography via tokens:** `font: var(--mat-sys-body-medium); letter-spacing: var(--mat-sys-body-medium-tracking);`.
5. **Spacing scale only:** 2, 4, 6, 8, 12, 16, 24, 32, 40, 48, 56, 64, 72, 80, 88, 96 → `--pdr-space-N`.
6. **Icons:** Material Symbols for generic UI (`<mat-icon fontSet="material-symbols-outlined">`), PDR SVG set for domain icons (`<mat-icon svgIcon="pdr:engine">`). Nothing else — see `references/foundations/icons.md`.
7. **Dark mode via `color-scheme`** only (`html.pdr-dark`). Never write per-component dark overrides.
8. **Wrappers are a last resort.** Create a `pdr-*` wrapper only when Material has no equivalent or PDR behavior is added (loading, status mapping). Wrappers compose Material; they never reimplement it.
9. **States are never hand-coded.** Figma Hovered/Focused/Pressed/Dragged = Material state layers.
10. **Unfinished pages:** 🔴 Accordion, Autocomplete; 🌕 Chips, Sheets, Status tags, Calendars, Chats, Files, Order preview, Payment, Popovers. Use Material defaults and flag deviations in the PR.
11. **Accessibility is a merge requirement:** WCAG 2.1 AA, keyboard-operable, labelled, ≥ 44 px targets — checklist in `references/foundations/accessibility.md`. Never put text on `secondary` or `warning` (light mode fails contrast); use their `-container` roles.
12. **Locked components — App bar and Page header.** Never change their design. App bar: used as-is, logo always SVG. Page header: only the title and the right-side page actions change; breadcrumbs appear automatically from navigation level 3. Details: `references/components/pdr/appbar-page-header.md`.
13. Ignore any Figma set prefixed `Deprecated/`, `Example/`, `.` or `_`.

## Figma → Angular mapping (index)

### ↓ ANGULAR MD3 COMPONENTS → `references/components/md3/`

| Figma page | File | Primary Angular API · wrapper |
|---|---|---|
| Accordion, Expansion panel 🔴 | `accordion-expansion-panel.md` | `mat-accordion`, `mat-expansion-panel` |
| Autocomplete 🔴 | `autocomplete.md` | `matAutocomplete`, `mat-autocomplete` |
| Badges | `badges.md` | `matBadge` |
| Button toggle (Segmented buttons) | `button-toggle.md` | `mat-button-toggle-group` |
| Buttons | `buttons.md` | `matButton`, `matIconButton`, `matFab` · `pdr-button` |
| Cards | `cards.md` | `mat-card appearance` |
| Checkboxes | `checkboxes.md` | `mat-checkbox` |
| Chips 🌕 | `chips.md` | `mat-chip-set/-listbox/-grid` · `pdr-dropdown-chip` |
| Data Grids | `data-grids.md` | `mat-table`, `matSort` · `pdr-cell-*` |
| Date & time pickers | `date-time-pickers.md` | `mat-datepicker`, `mat-date-range-picker`, `mat-timepicker` · `pdr-time-dial` |
| Dialogs | `dialogs.md` | `MatDialog` · `pdr-dialog-toolbar` |
| Divider | `divider.md` | `mat-divider` |
| Menus & Select | `menus-select.md` | `mat-select`, `mat-menu` |
| Navigation drawer & rail | `navigation-drawer-rail.md` | `mat-sidenav`, `mat-nav-list` |
| Paginators | `paginators.md` | `mat-paginator` |
| Progress indicators | `progress-indicators.md` | `mat-progress-bar`, `mat-progress-spinner` |
| Radio buttons | `radio-buttons.md` | `mat-radio-group` |
| Sheets 🌕 | `sheets.md` | `mat-sidenav`, `MatBottomSheet` · `pdr-side-sheet` |
| Sliders | `sliders.md` | `mat-slider` |
| Snackbar | `snackbar.md` | `MatSnackBar` |
| Switch | `switch.md` | `mat-slide-toggle` |
| Tabs, Steppers | `tabs-steppers.md` | `mat-tab-group`, `mat-tab-nav-bar`, `mat-stepper` |
| Text fields | `text-fields.md` | `mat-form-field`, `matInput` · `pdr-search-bar`, `pdr-code-input` |
| Toolbar | `toolbar.md` | `mat-toolbar.pdr-toolbar` |
| Tooltips | `tooltips.md` | `matTooltip` · `pdr-rich-tooltip` |
| Tree | `tree.md` | `mat-tree` |

### ↓ PDR COMPONENTS → `references/components/pdr/`

| Figma page | File | Wrappers |
|---|---|---|
| Alerts | `alerts.md` | `pdr-alert` |
| Appbar & Page header 🔒 | `appbar-page-header.md` | `pdr-app-bar`, `pdr-page-header` (locked), `pdr-top-app-bar` |
| Avatars | `avatars.md` | `pdr-avatar`, `pdr-avatar-group`, `pdr-selected-user` |
| Brand loader | `brand-loader.md` | `pdr-brand-loader` |
| Calendars 🌕 | `calendars.md` | `pdr-calendar-header`, `pdr-gantt-bar` |
| Chats, AI & Notes 🌕 | `chats-ai-notes.md` | `pdr-chat-message`, `pdr-message-input`, `pdr-note` |
| Files & Documents 🌕 | `files-documents.md` | `pdr-document-card`, `pdr-file-icon` |
| Megaoptions, ToDo | `megaoptions-todo.md` | `pdr-megaoption`, `pdr-todo-button` |
| Navigation menu (PDR) | `navigation-menu.md` | `pdr-side-nav`, `pdr-nav-item`, `pdr-menu-banner` |
| Order preview 🌕 | `order-preview.md` | `pdr-order-card`, `pdr-order-popover`, `pdr-workshop-status` |
| Panels & Widgets | `panels-widgets.md` | `pdr-panel`, `pdr-widget` |
| Payment & Invoices 🌕 | `payment-invoices.md` | `pdr-invoice-accordion`, `pdr-status-arrow` |
| Pickers | `pickers.md` | `pdr-color-picker`, `pdr-touchspin` |
| Popovers & Tipseens 🌕 | `popovers-tipseens.md` | `pdr-tipseen`, `pdr-module-popover` |
| Sign up & Login | `sign-up-login.md` | `pdr-auth-panel` |
| Skeleton loaders, empty and error states | `skeleton-empty-error-states.md` | `pdr-skeleton*`, `pdr-empty-state`, `pdr-error-state` |
| Status tags 🌕 | `status-tags.md` | `pdr-status-tag` + domain tags |
| Timelines | `timelines.md` | `pdr-timeline`, `pdr-history-row` |
| Toolbars (PDR) | `toolbars-pdr.md` | `pdr-order-toolbar`, `pdr-filter-bar` |
| Workflows | `workflows.md` | `pdr-wizard-steps`, `pdr-workflow` |
| WYSIWYG, Code, Drag-n-Drop | `wysiwyg-code-dnd.md` | `pdr-dropzone`, `pdr-wysiwyg`, `pdr-code-editor` |

### Foundations → `references/foundations/`

| Figma page | File | Contents |
|---|---|---|
| Grids and Breakpoints | `grids-breakpoints.md` | Breakpoints, column grids, layout regions, widget grid |
| ♿ Accessibility | `accessibility.md` | WCAG 2.1 AA checklist → Angular, measured token contrast, EAA / BFSG / BITV 2.0 |
| 24px Icons → PDR Icons | `icons.md` | Icon rules, PDR icon catalogue (69, Figma link + node IDs), export & `MatIconRegistry` setup |

### Examples → `references/examples/`

| Example | File |
|---|---|
| App shell | `app-shell.md` |
| Data grid page | `data-grid-page.md` |
| Settings page | `settings-page.md` |
| Filters | `filters.md` |
| Full-screen modal shell | `fullscreen-modal-shell.md` |
| Form modal / Summary modal | `form-modal.md`, `summary-modal.md` |
| Form sheet / Summary sheet | `form-sheet.md`, `summary-sheet.md` |

## Figma → token quick lookup

| Figma | Code |
|---|---|
| Variable `mat/sys/...` (e.g. `surface container/surface container low`) | `var(--mat-sys-surface-container-low)` |
| Variable `mat/sys/semantic/success/*`, `mat/sys/additional/*` | `var(--pdr-sys-success)`, `var(--pdr-sys-teal-container)` … |
| `Corner radius/` None · xs · s · m · l · xl · Full | `--mat-sys-corner-` none · extra-small · small · medium · large · extra-large · full |
| `space/space-N` | `var(--pdr-space-N)` |
| Effect style `M3/Elevation Light/N` | `var(--mat-sys-levelN)` |
| Text style `body/medium` etc. | `var(--mat-sys-body-medium)` + `-tracking` |
| `Modals/S…XXXL` | `--pdr-dialog-width-s…xxxl` (see `md3/dialogs.md`) |
| `Breakpoints/XS…XXL` | `PDR_BREAKPOINTS` (XS < 576 · S 576 · M 768 · L 992 · XL 1200 · XXL 1600) — see `references/foundations/grids-breakpoints.md` |

## Workflow

1. Read the frame via Figma MCP (`get_design_context`, `get_variable_defs`).
2. Map bound variables → tokens (table above / `tokens.json`).
3. Start from an example in `references/examples/`. Find each Figma component in the index; open `references/components/{md3|pdr}/<page>.md` for variant APIs and overrides.
4. Apply only overrides defined in the component file or `theming-rules.md`; add new ones to the component file's Overrides section, never inline.
5. Verify light + dark (`html.pdr-dark`), keyboard-only use, 200 % text / 400 % zoom, and widths 320 / 375 / 768 / 992 / 1200 / 1600. Run `pnpm test` (axe).
