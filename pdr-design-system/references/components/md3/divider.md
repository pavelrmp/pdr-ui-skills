# Divider

Figma page: **Divider 🟢** `10808:983` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10808-983) · Figma Spec: [`10990:1510`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10990-1510)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Divider`, `Divider with subheader` · **Angular:** `<mat-divider>` · **Sources:** [M3 Divider overview](https://m3.material.io/components/divider/overview), [guidelines](https://m3.material.io/components/divider/guidelines), [specs](https://m3.material.io/components/divider/specs)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

A divider is a thin line that groups content in lists and containers.

**Use a divider when**

- Items **can’t** be grouped with open space alone.
- Larger sections of unrelated content need separating (full-width).
- Interactive and non-interactive areas of a container (e.g. a card) need separating (full-width).
- Related or nested items within a section need separating (inset).

**Don’t use a divider when**

- Spacing, headlines or grouping already make the structure clear — prefer whitespace.
- It would separate every individual item (e.g. each destination in a navigation drawer).
- It would follow every piece of content on a page.

**Alternatives:** whitespace (default), a subheader, or a gap (menus).

## Anatomy

| # | Element | Required | Notes |
|---|---|---|---|
| 1 | Line | Yes | 1 px, color `outline-variant` |
| 2 | Inset margin | No | Leading (Inset) or both sides (Middle inset) |
| 3 | Subheader | No | Only in `Divider with subheader` — label text below the line |

## Figma component and properties

| Component | Property | Values | Angular |
|---|---|---|---|
| Divider | Orientation | Horizontal, Vertical | `[vertical]="true"` for Vertical |
| Divider | Inset | None, Inset, Middle inset | `[inset]="true"` for Inset; Middle inset needs a custom margin |
| Divider with subheader | Subheader (text) | Any short label | `<mat-divider>` + subheader element |

Horizontal dividers fill the width of their container; vertical dividers fill the height of their row.

## Decision rules

1. **MUST** first check whether whitespace alone groups the content. Add a divider only if it doesn’t.
2. To separate **different kinds of content** or **larger unrelated sections** → `Inset=None` (full-width).
3. To separate **interactive from non-interactive areas** of a container (e.g. card body vs. a “read more” action) → `Inset=None`.
4. To separate **related or nested items within a section** → `Inset=Inset`.
5. To separate related content **inside a container with padding on both sides** → `Inset=Middle inset`.
6. To separate **horizontally arranged** content or regions (e.g. a rail from app content, inline actions) → `Orientation=Vertical`.
7. **SHOULD** combine full-width and inset dividers to reflect the information hierarchy (full-width for sections, inset for items within them).
8. **SHOULD** use full-width dividers sparingly.
9. **MUST NOT** use dividers to separate every individual item; group things instead.

## Behavior and interaction

Dividers are static and non-interactive. They don’t respond to hover, focus or press, and they don’t move or animate.

## States

None. The divider has a single appearance.

## Content guidelines

- Make dividers visible but not bold — never thicker than 1 px or darker than `outline-variant`.
- In `Divider with subheader`, keep the subheader to a short section label.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use full-width dividers to separate unrelated sections | Add a full-width divider after every piece of content |
| Use inset dividers for related items inside a section | Use dividers to separate each destination in a navigation drawer |
| Use full-width dividers to separate groups of navigation destinations | Use the `outline` color role for dividers |
| Prefer whitespace when it already groups the content | Use dividers as decoration |

## Combining with other components

- **Lists:** inset dividers between related items; full-width between groups.
- **Cards:** full-width for content that can expand or to separate actions; inset for related content.
- **Navigation drawer:** full-width dividers between groups of destinations, never between single destinations.
- **Navigation rail:** an optional vertical divider on the rail edge next to the content area.
- **Menus:** on web, a divider MAY separate groups of menu items.
- **Dialogs, tabs, side sheets:** these components include their own optional dividers — use the component’s divider, not a separate one.
- **Tables (PDR):** see Data Grids › Key principles — tables avoid row dividers unless the table falls apart without them.

## Accessibility

- Color `outline-variant` is intended for dividers. **MUST NOT** use `outline`, which has different contrast requirements.
- A divider never carries meaning on its own — group content with headings or subheaders as well.

## Measurements and tokens

| Attribute | Value | Token |
|---|---|---|
| Thickness | 1 px | — |
| Color | outline-variant | `--mat-sys-outline-variant` |
| Full-width | 100% of the container | — |
| Inset — leading margin | 16 px | `--pdr-space-16` |
| Inset — trailing margin | 0 px | — |
| Middle inset — leading and trailing margin | 16 px each | `--pdr-space-16` |
| Space between divider and supporting text | 4 px | `--pdr-space-4` |

## AI checklist

- [ ] Whitespace alone isn’t enough → divider justified
- [ ] Full-width for sections, inset for related items, middle inset inside padded containers
- [ ] Vertical only between horizontally arranged regions
- [ ] Not used between every item
- [ ] Color `outline-variant`, 1 px, no states

## Not covered by M3 (PDR conventions)

- **Vertical inset values:** M3 lists no vertical inset values. The Figma component uses 8 px top (Inset) and 8 px top and bottom (Middle inset).
- **Angular inset:** Angular’s `[inset]` margin may differ from the 16 px above. Verify it in code.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Horizontal | `<mat-divider>` |
| Vertical | `<mat-divider [vertical]="true">` (parent must stretch height) |
| Inset=Inset | `[inset]="true"` (inside `mat-list`) |
| Inset=Middle inset | `class="pdr-divider--middle"` |
| Divider with subheader | `<mat-divider>` + `<div mat-subheader>Title</div>` |

### Overrides (`styles/components/md3/_divider.scss`)

```scss
// Figma Inset=Middle inset (16px both sides)
.pdr-divider--middle { margin-inline: var(--pdr-space-16); }
```
