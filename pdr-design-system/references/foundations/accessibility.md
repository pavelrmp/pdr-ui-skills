# Accessibility

Figma page: **♿ ACCESSIBILITY 🌕** `5202:17588` · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=5202-17588)
Frames: Accessibility Check List `5706:41746`, Design Check List `5706:42357`, European Accessibility Act `5716:49244`.

> 🌕 The Figma page is still in progress. The checklist below is the team's agreed baseline; treat every item as a **merge requirement**.

## Target & legal basis

**WCAG 2.1 level AA** is the minimum for every PDR.cloud screen. Legal background (from the Figma page):

| Source | Scope |
|---|---|
| [Directive (EU) 2019/882 — European Accessibility Act](https://eur-lex.europa.eu/eli/dir/2019/882/oj?locale=en) | EU accessibility requirements for products and services |
| [Barrierefreiheitsstärkungsgesetz (BFSG)](https://www.bundesfachstelle-barrierefreiheit.de/DE/Fachwissen/Produkte-und-Dienstleistungen/Barrierefreiheitsstaerkungsgesetz/barrierefreiheitsstaerkungsgesetz_node.html) | German implementation of the EAA |
| [BITV 2.0](https://www.gesetze-im-internet.de/bitv_2_0/BJNR184300011.html) | German regulation for accessible IT (references EN 301 549 / WCAG) |
| [Standardanforderungskatalog](https://www.barrierefreiheit-dienstekonsolidierung.bund.de/Webs/PB/DE/standardanforderungskatalog/standardanforderungskatalog-node.html) | Federal catalogue of concrete test requirements |

This is a summary for developers, not legal advice; questions about obligations go to product/legal.

## Checklist (Figma "Accessibility Check List") → Angular implementation

### Generic / mobile
| Requirement | How in PDR Angular |
|---|---|
| Works in portrait **and** landscape | No orientation locks; test both on mobile breakpoints (`grids-breakpoints.md`). |
| Usable at **320 px** viewport width | Layout must reflow at 320 px (narrower than the 375 design frame). No fixed min-widths on page containers. |
| Page never scrolls horizontally | Only data-grid comparison tables may scroll inside their own container (see `../components/md3/data-grids.md`). |
| Touch targets **≥ 44 × 44 px** (except inline text links) | Material controls give 48 px targets at density 0 — never use negative density on touch layouts. Custom `pdr-*` controls: min 48 px. |
| Viewport zoom not disabled | `<meta name="viewport" content="width=device-width, initial-scale=1">` — never `maximum-scale` / `user-scalable=no`. |

### Color & contrast
| Requirement | How |
|---|---|
| Text ≥ **4.5:1**; UI components & graphics ≥ **3:1** | Use only token pairs (`on-X` on `X`, `on-X-container` on `X-container`). See measured table below for the exceptions. |
| Tested with a color-blindness simulator | Chrome DevTools → Rendering → "Emulate vision deficiencies", or the Figma plugins below. |
| Color is never the only signal | Status tags always have text or an icon + `aria-label`; error fields show `<mat-error>` text; overdue rows have an icon/text cue (see `../examples/data-grid-page.md`). |

#### Measured contrast of PDR token pairs (light / dark)

| Pair | Light | Dark | Verdict |
|---|---|---|---|
| on-primary / primary | 5.40 | 6.33 | ✅ |
| on-primary-container / primary-container | 7.53 | 10.20 | ✅ |
| **on-secondary / secondary** | **2.42** | 5.53 | ❌ light — never put text on `secondary`; use `secondary-container` |
| on-tertiary / tertiary | 9.57 | 9.57 | ✅ |
| on-error / error | 4.98 | 5.94 | ✅ |
| on-surface / surface | 19.30 | 19.30 | ✅ |
| on-surface-variant / surface | 9.78 | 13.62 | ✅ |
| primary (links) / surface | 5.16 | 9.28 | ✅ |
| outline / surface | 4.50 | 4.29 | ✅ (field borders, ≥ 3:1) |
| outline-variant / surface | 1.42 | 1.97 | ⚠️ decorative only (dividers) — never the only boundary of an input or control |
| on-success / success | 5.16 | 7.07 | ✅ |
| **on-warning / warning** | **2.72** | 8.07 | ❌ light — use `warning-container` + `on-warning-container` (7.93) for any text |
| **warning / surface** | **2.60** | 11.44 | ❌ light — warning color alone is not enough for icons/borders; pair with `on-warning-container` text |
| error / surface | 4.76 | 7.40 | ✅ |
| on-surface-disabled / surface | 2.43 | 4.29 | exempt (disabled, WCAG 1.4.3) |
| all `on-*-container` / `*-container` (success, info, warning, error) | ≥ 7.5 | ≥ 10 | ✅ |

Report the ❌ rows to design; until fixed, the workarounds in the Verdict column are mandatory.

### Forms
| Requirement | How |
|---|---|
| Every input has a label | `<mat-label>` inside `mat-form-field` (Material wires `for`/`id`). Placeholder is never the label. Inputs without visible label → `aria-label`. |
| `<fieldset>` + `<legend>` for groups | Radio groups / related checkboxes: `<fieldset>` with `<legend>` (visually styled as title-small), or `mat-radio-group` with `aria-labelledby`. |
| `autocomplete` where appropriate | `autocomplete="name|email|tel|street-address|postal-code|username|current-password|one-time-code"`. |
| Error messages are associated with inputs | Use `<mat-error>` (Material sets `aria-describedby`); custom controls must set `aria-describedby` + `aria-invalid`. |

### Images & icons
| Requirement | How |
|---|---|
| Every `<img>` has `alt` | Meaningful → describe; decorative → `alt=""`. Avatars: see `../components/pdr/avatars.md`. |
| Complex charts have text alternatives | Provide a data table or summary (axes, values, labels) next to/under the chart. |
| Decorative SVG/icons are hidden | `<mat-icon aria-hidden="true">` (Material default for font icons) — PDR SVG icons too (`icons.md`). |
| Informative SVG has `role="img"` + label | Standalone meaningful icon: `<mat-icon svgIcon="pdr:engine" role="img" aria-label="Motor">`; icon-only buttons put the label on the button. |

### Keyboard
| Requirement | How |
|---|---|
| Everything works with keyboard only | Use native `<button>`/`<a>` and Material components; custom widgets use CDK (`ListKeyManager`, `CdkStepper`, `cdkTrapFocus`). |
| Visible focus on all interactive elements | Keep Material focus indicators; custom elements: `:focus-visible { outline: 2px solid var(--mat-sys-primary); outline-offset: 2px; }`. Never `outline: none` without a replacement. |
| Focus order = visual order | DOM order matches layout; never reorder with CSS `order`/absolute positioning for interactive content. |
| No invisible focusable elements | Hidden content uses `@if` / `hidden`, not `opacity: 0` / off-screen positioning. |
| Buttons react to Space and Enter | Use `<button>`; never `(click)` on `div`/`span`. |
| Dialogs/overlays close with Esc | Default for `MatDialog`, `mat-menu`, `MatBottomSheet`, `cdkConnectedOverlay` (`(overlayKeydown)`). Don't set `disableClose` unless there are unsaved changes — then Esc opens the confirm dialog. |

### Markup
| Requirement | How |
|---|---|
| Valid HTML | Lint templates (`@angular-eslint/template` accessibility rules enabled). |
| `<html lang>` correct | `lang="de"` (or the active locale) — update on language switch via `DOCUMENT`. |
| Unique `<title>` per page | Route `title` property or `TitleStrategy`: `"<Page> · PDR.cloud"`. |
| Landmarks | `pdr-app-bar` → `<header>`, navigation → `<nav aria-label>`, page → `<main>`, footer → `<footer>`. |
| `tabindex` only `0` or `-1` | Never positive values. |
| No `autofocus` attribute | Focus programmatically (`cdkFocusInitial`, `autoFocus: 'first-tabbable'`, `FocusMonitor.focusVia`). |
| No `title` attribute tooltips | Use `matTooltip` (accessible) — never `title=""`. |
| `<a href>` for links, `<button>` for actions | Navigation → `<a routerLink>` (`matButton` works on `<a>`); actions → `<button>`. |
| Tables use `<table>`, `<th>`, `<caption>` | `mat-table` on native `<table>`; add `<caption class="cdk-visually-hidden">` describing the table. Mobile list views stay lists. |

### Content
| Requirement | How |
|---|---|
| Plain, clear language | German UI copy at roughly 8th-grade reading level; no jargon without explanation (abbreviations get `matTooltip`, see data grids). |
| Unique, descriptive link/button text | No "hier klicken" / "mehr"; icon-only buttons have specific `aria-label`s ("Auftrag A0001232 löschen"). |
| One `<h1>` per page | `pdr-page-header` renders the only `<h1>`. |
| Headings in logical order, no skipped levels | Panel titles `<h2>`, sections inside `<h3>`; style via typography tokens, not heading level. |
| Lists use `<ol>/<ul>/<dl>` | Including card grids and definition-style summaries (`dl` in summary modals/sheets). |
| Keyboard-focusable skip link | First element in `app.component`: `<a class="pdr-skip-link" href="#main">Zum Inhalt springen</a>`, visible on focus. |
| Main reading text line height ≥ 1.5× | `body-large` (16/24 = 1.5) meets it; `body-medium` (14/20 ≈ 1.43) does not — use `body-large` for long-form reading text (notes, descriptions, chat), `body-medium` only for compact UI text. |

### Testing (definition of done)
| Check | Tool |
|---|---|
| Automated tests pass | `pnpm test` in the project root (includes axe) |
| Manual automated scan | axe DevTools Chrome extension |
| Screen readers | NVDA (Windows), JAWS (Windows), VoiceOver (macOS), TalkBack (Android) |
| Windows high contrast mode | `@media (forced-colors: active)` — don't rely on backgrounds/box-shadows for meaning; borders must stay visible |
| Text size 200 % and zoom 400 % | Chrome text size setting; Cmd/Ctrl + `+` up to 400 % (content reflows, no loss) |

## Design check (Figma "Design Check List")
Before handoff, designers run [axe for Designers](https://www.figma.com/community/plugin/1085612091163821851/axe-for-designers-a-free-accessibility-plugin) and the [WCAG Plugin](https://www.figma.com/community/plugin/1373362852131056921/wcag-plugin). Developers may ask for the plugin report when a frame contains new color combinations.

## Angular helpers
```ts
import { LiveAnnouncer } from '@angular/cdk/a11y';
// announce async results that have no visible focus change
inject(LiveAnnouncer).announce('3 Aufträge gefunden', 'polite');
```
```scss
.pdr-skip-link {
  position: absolute; left: var(--pdr-space-16); top: -100px;
  padding: var(--pdr-space-8) var(--pdr-space-16);
  background: var(--mat-sys-primary); color: var(--mat-sys-on-primary);
  border-radius: var(--mat-sys-corner-small); z-index: 1000;
}
.pdr-skip-link:focus { top: var(--pdr-space-8); }
@media (prefers-reduced-motion: reduce) { *, *::before, *::after { animation-duration: .01ms !important; transition-duration: .01ms !important; } }
```
The reduced-motion rule is the **only** permitted `!important` in the codebase (global, in `styles.scss`).
