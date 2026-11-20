# Tabs

Figma page: **Tabs 🟢** `3330:127` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-127) · Figma Spec: [`11009:2372`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11009-2372)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Tab`, `Tabs` · **Angular:** `<mat-tab-group>` / `<nav mat-tab-nav-bar>` · **Sources:** [M3 Tabs guidelines](https://m3.material.io/components/tabs/guidelines), [Navigation bar guidelines](https://m3.material.io/components/navigation-bar/guidelines), [Badges guidelines](https://m3.material.io/components/badges/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Tabs organise related content across views **within a page**.

| Type | Use |
|---|---|
| Primary tabs | The page’s main content destinations, at the top of the content under the app bar |
| Secondary tabs | Further separate related content inside a content area; **always placed below primary tabs** |

**Use navigation (rail, drawer, bar) for distinct pages, and tabs for related content within a page.**

## Anatomy

Container · tab (label and/or icon) · active indicator · badge (optional) · divider.

## Figma components and properties

| Component | Properties |
|---|---|
| Tab | Type Primary / Secondary · Selected True/False · State Enabled, Hovered, Focused, Pressed, Disabled · Show icon · Show status (badge) · Show trailing icon + Instance |
| Tabs | Type Primary / Secondary · Show mask left · Show mask right — scroll arrows (‹ ›) when the tabs don’t fit (Angular tab pagination) |

## Decision rules

1. Main content destinations of a page → `Type=Primary`. Related content inside a content area → `Type=Secondary`, always placed below primary tabs. Don’t mix both types in one row.
2. Exactly one tab `Selected=True` in a set.
3. All tabs fit → **fixed** tabs (all shown at once); turn the masks off. They don’t fit → **scrollable** tabs; turn on `Show mask left/right` to show the scroll arrows.
4. **SHOULD NOT** truncate tab labels — truncation confuses people; use scrollable tabs instead.
5. Secondary tabs **MUST** sit below primary tabs, never above.
6. Badges on tabs show updates; update or remove the badge once the content was viewed.
7. Fewer than three top-level destinations on mobile → tabs, not a navigation bar.

## Behavior

Select a tab to switch content; fixed tabs MAY also be switched by swiping the content area (touch).

## States

Enabled, Hovered (on-surface state layer 8 %), Focused (12 % + 1 px primary ring), Pressed (12 %), Disabled (38 % opacity) — each with Selected True/False and Type Primary/Secondary.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use tabs for related content within one page | Use tabs to navigate between distinct pages |
| Use scrollable tabs for many or long labels | Truncate tab labels |
| Place secondary tabs below primary tabs | Use tabs for a linear multi-step task — use a Stepper |

## AI checklist

- [ ] Tabs for related content, navigation for pages
- [ ] One selected tab; fixed or scrollable chosen by fit
- [ ] No truncated labels
- [ ] Secondary tabs below primary

## Not covered

- **Keyboard interaction:** not covered by the sources used here. Follow Angular `mat-tab-group` defaults.
- **Primary row:** tabs share the row width equally (fixed tabs). For scrollable primary tabs, set the tabs to hug their content and turn the masks on.

---

# Part 2 — Angular implementation

### Mapping
| Figma | Angular |
|---|---|
| Tabs (content switching) | `<mat-tab-group [(selectedIndex)] mat-stretch-tabs="false" mat-align-tabs="start">` + `<mat-tab label>` |
| Tabs (routing) | `<nav mat-tab-nav-bar [tabPanel]="panel">` + `<a mat-tab-link routerLinkActive [active]>` + `<mat-tab-nav-panel #panel>` |
| Selected=True | `selectedIndex` / `active` |
| Tab with badge/icon | `<ng-template mat-tab-label>` |

Lazy tab content: `<ng-template matTabContent>`.

| Type=Secondary | second `<mat-tab-group>` / `nav mat-tab-nav-bar` inside the content area, **below** the primary tabs |
| Show mask left/right (scroll arrows) | automatic Angular tab pagination when tabs overflow; keep `mat-stretch-tabs="false"` |
| Show status (badge) | `<ng-template mat-tab-label>Label <span matBadge="3" matBadgeOverlap="false"></span></ng-template>` |

### Overrides

None — Figma matches M3 defaults. Do not add any.
