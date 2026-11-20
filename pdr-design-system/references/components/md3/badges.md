# Badges

Figma page: **Badges 🟢** `10745:46595` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10745-46595) · Figma Spec: [`10993:2401`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10993-2401)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma component:** `Badge` · **Angular:** `matBadge` directive · **Sources:** [M3 Badges guidelines](https://m3.material.io/components/badges/guidelines), [specs](https://m3.material.io/components/badges/specs), [Navigation bar](https://m3.material.io/components/navigation-bar/guidelines), [Navigation rail](https://m3.material.io/components/navigation-rail/guidelines), [Tabs](https://m3.material.io/components/tabs/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Badges indicate a notification, an item count, or other information relating to a navigation destination or icon.

**Use when**

- A destination or icon has an unread update → small badge.
- The number of updates matters → large badge with a count.

**Don’t use when**

- (PDR) The information is the status of a record (e.g. “Bezahlt”) → use a Status tag.

## Anatomy

| # | Element | Notes |
|---|---|---|
| 1 | Small badge | A simple circle, no label |
| 2 | Large badge container | Holds the label |
| 3 | Large badge label | Count or short text, 1–4 characters |

## Figma component and properties

| Property | Values | Use |
|---|---|---|
| Size | Small | Unread indicator, no label |
| Size | Large | Count, 1–4 characters |
| Size | XLarge | PDR extension (not M3) |
| Label text | Text | Count for Large / XLarge |

## Decision rules

1. Indicate **that** there is something new → `Size=Small` (no label).
2. Show **how many** → `Size=Large` with the count.
3. **MUST** limit large badge content to **4 characters, including a “+”** (e.g. “999+”).
4. **MUST** place badges on navigation items or icons:
   - **Navigation bar and compact rail:** upper-right corner of the icon, overlapping it.
   - **Expanded rail:** next to the label text.
5. **SHOULD** update the badge value, or remove the badge, once the person has viewed the related content.
6. In right-to-left languages, the badge mirrors to the upper-left corner of the icon.

## Behavior and interaction

Badges aren’t interactive. They change value or disappear when the underlying content changes.

## States

None. The badge has no interaction states.

## Content guidelines

- Numbers only, or very short text; maximum 4 characters including “+”.

## Usage guidelines

| Do | Don’t |
|---|---|
| Use a small badge to indicate an update | Use more than 4 characters |
| Use a large badge for a count | Keep showing the badge after the content was viewed |
| Place the badge on the icon of a navigation item | (PDR) Use a badge for record status — use Status tags |

## Combining with other components

- **Navigation bar, navigation rail, tabs:** both small and large badges are allowed.
- **Icon buttons:** a badge MAY sit on an icon button, e.g. notifications in the app bar.

## Measurements

| Attribute | Value |
|---|---|
| Small badge size | 6 × 6 px, corner radius 3 px |
| Large badge height | 16 px, corner radius 8 px |
| Large badge, one digit | 16 × 16 px |
| Large badge, max characters | 16 × 34 px |
| Large badge horizontal padding | 4 px |
| Small badge offset | 6 × 6 px from the icon’s top trailing corner |

## AI checklist

- [ ] Small = indicator, Large = count
- [ ] Max 4 characters including “+”
- [ ] Placed on a navigation item or icon, upper-right (mirrored in RTL)
- [ ] Not used for record status

## Not covered by M3 (PDR conventions)

- **`Size=XLarge`:** a PDR extension with no M3 definition. Use it only where the PDR design requires it.
- **Badge accessibility:** M3 gives no specific labeling guidance in the sources used here.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Size=Small (6px dot) | `matBadge="" matBadgeSize="small"` |
| Size=Large (16px, 1–2 digits) | `[matBadge]="count"` (default size) |
| Size=XLarge (auto width, e.g. "99+") | `[matBadge]="count > 99 ? '99+' : count"` (default size grows) |
| Hidden at 0 | `[matBadgeHidden]="count === 0"` |

Always add `matBadgeDescription` for screen readers. Color is `error` by default in M3 — no `matBadgeColor`.

### Overrides


None — Figma matches M3 defaults. Do not add any.
