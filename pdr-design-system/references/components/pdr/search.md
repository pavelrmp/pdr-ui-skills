# Search

Figma page: **Search 🟢** `10998:41924` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10998-41924) · Figma Spec: [`11037:9670`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11037-9670)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Search bar`, `Search view full-screen`, `Search result` · **Angular:** custom PDR components following M3 Search (selectors to confirm) · **Sources:** [M3 Search guidelines](https://m3.material.io/components/search/guidelines), [M3 Search specs](https://m3.material.io/components/search/specs), [Search accessibility](https://m3.material.io/components/search/accessibility); component descriptions on this page

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Search lets people enter a keyword or phrase and get relevant information. It’s an alternative to other forms of navigation.

| Need | Use |
|---|---|
| Search contents of a specific view (e.g. “Search your messages”) | `Search bar` — a persistent, prominent field at the top of the screen |
| Show suggestions and results while searching | Search view: **full-screen** on compact screens, **docked** below the bar on larger screens |
| Pick a value for a form field from a long list | Autocomplete (not Search) |

## Figma components and properties

| Component | Properties |
|---|---|
| Search bar | Placeholder text · State: Enabled, Hovered, Pressed · Show avatar |
| Search view full-screen | Placeholder text · Input text · Label text: Input text, Supporting text · List items: False, True |
| Search result | 1-line list item with avatar or thumbnail; trailing items toggle on/off |

## Decision rules

1. Use `Search bar` when search is a primary action of the screen; place it at the top of the content it searches.
2. When focused, suggestions and results appear in a list below the search bar.
3. **Compact screens (mobile)** → full-screen layout (`Search view full-screen`). **Larger screens** → docked layout: a list below the search bar with a scrim over the main content. Search **MUST** swap from full-screen to docked at larger breakpoints.
4. Docked results: min height 240 px, max ⅔ of the screen height.
5. Use `Search result` rows for suggestions and results (one line, leading avatar or thumbnail).
6. The placeholder names what is searched (e.g. “Aufträge durchsuchen”). *(PDR proposal — confirm)*

## Measurements

| Attribute | Value |
|---|---|
| Search bar height | 56 px |
| Leading / trailing padding | 16 px |
| Docked results height | Min 240 px, max ⅔ of screen height |

## Accessibility

- When suggestions or results appear, screen readers **MUST** be informed (announce the updated results).

## AI checklist

- [ ] Search bar at the top of the searched content
- [ ] Full-screen on mobile, docked on larger screens
- [ ] Results as Search result rows
- [ ] Autocomplete instead of Search for form values

## Open questions for the team

- **Docked layout:** there’s no docked search view component, only `Search view full-screen`. Should a docked version be built for desktop?
- **Deprecated layers:** `Search bar` and `Search view full-screen` still contain `Deprecated/…` layers. Swap them to current components.

---

# Part 2 — Angular implementation

### Mapping
| Figma | Angular |
|---|---|
| Search bar | `<pdr-search-bar [placeholder] [avatar]>` — 56 px, `corner-extra-large`, `surface-container-lowest`, body-large |
| Search view full-screen (mobile) | `MatDialog` full-screen (`../md3/dialogs.md`) containing the input + results list |
| Docked results (≥ M breakpoint) | `cdkConnectedOverlay` below the bar, with backdrop (scrim); min 240 px, max ⅔ viewport height |
| Search result | `<mat-nav-list>` rows (`lines="1"`, `matListItemAvatar` / thumbnail) — see `../md3/list.md` |
| Form value from a long list | **not** Search → `../md3/autocomplete.md` |

```ts
// switch layout by breakpoint (spec rule 3)
open() { this.bp.isMatched(PDR_BREAKPOINTS.mobile) ? this.openFullscreen() : this.docked.set(true); }
// announce results (spec: Accessibility)
effect(() => inject(LiveAnnouncer).announce(`${this.results().length} Ergebnisse`, 'polite'));
```

### Overrides
```scss
.pdr-search-bar {
  height: 56px; padding-inline: var(--pdr-space-16);
  border-radius: var(--mat-sys-corner-extra-large);
  background: var(--mat-sys-surface-container-lowest);
  font: var(--mat-sys-body-large);
}
.pdr-search-results { min-height: 240px; max-height: 66.67dvh; overflow-y: auto; }
```
