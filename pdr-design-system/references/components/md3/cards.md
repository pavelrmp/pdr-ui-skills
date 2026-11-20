# Cards

Figma page: **Cards 🟢** `10826:959` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10826-959) · Figma Spec: [`10995:1747`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10995-1747)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma component:** `Card` · **Angular:** `<mat-card>` · **Sources:** [M3 Cards guidelines](https://m3.material.io/components/cards/guidelines), [Cards accessibility](https://m3.material.io/components/cards/accessibility), [Elevation tokens](https://m3.material.io/styles/elevation/tokens), [Color roles](https://m3.material.io/styles/color/roles)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Cards display content and actions about a single subject.

**Use when** content about one subject (an order, a customer, a vehicle) needs to be grouped and scanned as a unit, often in a collection.

**Don’t use when** spacing, headlines or dividers would create a simpler visual hierarchy. Don’t force content into cards.

**Collections:** cards MAY be grouped in a grid, a list or a carousel.

## Anatomy

| # | Element | Required |
|---|---|---|
| 1 | Container | Yes — the only required element |
| 2 | Header (avatar, title, subtitle, ⋮ menu) | No |
| 3 | Media | No |
| 4 | Headline | No |
| 5 | Supporting text | No |
| 6 | Actions (buttons) | No |
| 7 | Divider | No |

## Figma component and properties

| Property | Values |
|---|---|
| Style | Elevated, Filled, Outlined |
| State | Enabled, Hovered, Pressed, Dragged, Disabled |
| Show header · Show media · Show headline · Show supporting text · Show actions | Toggles |
| Title · Subtitle · Headline · Supporting text | Text |

Avatar, ⋮ button, action buttons and the image placeholder are nested instances you can adjust.

## Decision rules

1. **Choose the style by emphasis:**
   - `Style=Filled` → subtle separation from the background; least emphasis.
   - `Style=Elevated` → a drop shadow gives more separation than Filled.
   - `Style=Outlined` → a visual boundary gives the most emphasis of the three.
2. **MUST** choose one interaction model per card:
   - **Directly actionable** — the whole card opens/does something; **no buttons or links inside**.
   - **Non-actionable** — the card itself does nothing; actions are buttons or links inside it.
   **MUST NOT** place an action on an actionable surface (no buttons inside a clickable card).
3. Use `State=Hovered / Pressed / Dragged` only for directly actionable cards. Non-actionable cards have **no hover state**.
4. Show only the slots the content needs; the container is the only required element.
5. Use full-width dividers for content that can expand; inset dividers to separate related content.

## Behavior and interaction

- Directly actionable card: clicking shows a ripple and performs the action.
- Cards MAY expand to reveal more content (container transform). Reserve this for expressive hero moments.

## States

| State | Applies to |
|---|---|
| Enabled | All cards |
| Hovered, Pressed | Directly actionable cards only |
| Dragged | Cards that can be reordered |
| Disabled | Directly actionable cards that are currently unavailable |

## Content guidelines

- One subject per card.
- (PDR) Headline first, supporting text short; actions at the end.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use one interaction model per card | Put buttons inside a clickable card |
| Use cards for one subject each | Wrap everything in cards when spacing would do |
| Use `outline-variant` for the Outlined card border | Use the `outline` color role for cards |

## Accessibility

- All actionable elements **MUST** get screen-reader and keyboard focus.
- Directly actionable cards are tab stops and have the **button** or **link** role.
- Non-actionable cards aren’t tab stops; every actionable element inside them is, and all are visited before focus moves to the next card.
- **Tab** moves to the next actionable element (or the next card container for directly actionable cards).

## Measurements and tokens

| Attribute | Value |
|---|---|
| Elevated card | Elevation level 1 (1 dp), container `surface-container-low` |
| Filled and Outlined cards | Elevation level 0 |
| Outlined card border | `outline-variant` |
| Corner radius (Figma) | 12 px, `--mat-sys-corner-medium` |

## AI checklist

- [ ] Card used for one subject, not as decoration
- [ ] Style chosen by emphasis
- [ ] Either directly actionable **or** contains buttons — never both
- [ ] No hover state on non-actionable cards
- [ ] Border uses outline-variant

## Not covered by M3 (PDR conventions)

- **Filled in Angular:** Angular’s `<mat-card>` documents `appearance="raised"` and `"outlined"`. Confirm with development that Filled is supported in your Angular version.
- **Dark theme shadows:** Figma uses the light elevation styles. Dark-theme screens need the dark elevation styles applied manually.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Style=Elevated | `<mat-card appearance="raised">` |
| Style=Filled | `<mat-card appearance="filled">` |
| Style=Outlined | `<mat-card appearance="outlined">` |
| Header / media / actions | `<mat-card-header>` (`mat-card-avatar`, `<mat-card-title>`, `<mat-card-subtitle>`), `<img mat-card-image>`, `<mat-card-content>`, `<mat-card-actions align="end">` |
| State=Hovered/Pressed (clickable card) | wrap card in `<a>`/`<button class="pdr-card--interactive">`; never put `(click)` on `mat-card` |
| State=Dragged | `cdkDrag` on the card; `cdkDragPreview` gets level4 |
| State=Disabled | `aria-disabled="true"` + `pdr-card--disabled` on wrapper |

### Overrides (`styles/components/md3/_cards.scss`)

```scss
.pdr-card--interactive { display: block; border-radius: var(--mat-sys-corner-medium); text-decoration: none; color: inherit; }
.pdr-card--interactive:focus-visible { outline: 2px solid var(--mat-sys-primary); outline-offset: 2px; }
.pdr-card--disabled { opacity: .38; pointer-events: none; }
```
Container colors/shape = M3 defaults — do not override.
