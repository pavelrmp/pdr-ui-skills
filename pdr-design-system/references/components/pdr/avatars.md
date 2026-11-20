# Avatars

Figma page: **Avatars 🟢** `3562:3774` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3562-3774) · Figma Spec: [`11032:4829`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11032-4829)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Avatar`, `Avatar group`, `Substitute avatar` · **Angular:** custom PDR component built on Angular Material tokens (selector to confirm) · **Sources:** component properties and descriptions on this page; [M3 Lists](https://m3.material.io/components/lists/guidelines) (avatars as leading elements)

> **No M3 component.** M3 uses avatars only inside other components (lists, chips). Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Avatars represent a person, company or role. In PDR the **category** of an avatar shows what kind of contact it is — a private customer, an insurer, an expert — so people can recognise contacts at a glance.

## Figma components and properties

| Component | Properties |
|---|---|
| Avatar | Category: Privatkunde, Geschäftskunde, Autohaus, Sachverständiger, Rechtsanwalt, Versicherung, Leasing, Fahrer, Support Team, PDR Bot, AI, Monogram, Photo, Add new, Placeholder Phase 1 · **Size: 32, 40, 48, 64, 80, 96** (px) · Show status |
| Avatar group | Type: Placeholder, Initials, Mix · 80 × 32 px |
| Substitute avatar | Shows a substitute (Vertretung) for a person |

## Decision rules

1. **Contact types:** use the `Category` that matches the contact type (Privatkunde, Geschäftskunde, Versicherung, Sachverständiger, Rechtsanwalt, Autohaus, Leasing, Fahrer). **MUST NOT** mix up types.
2. **Real people:** `Photo` when a photo is available; otherwise `Monogram` (initials). *(PDR proposal — confirm)*
3. **System actors:** `PDR Bot` for automated system messages; `AI` for the AI assistant; `Support Team` for PDR support. *(PDR proposal — confirm)*
4. `Add new` only as the action to add a contact or person; `Placeholder Phase 1` only as a placeholder while data is missing.
5. `Avatar group` for several people on one record (e.g. a team on an order). Show at most a few avatars and a “+n” overflow. *(PDR proposal — confirm)*
6. `Show status` adds a status indicator (e.g. presence). Use it only where the status matters in context. *(PDR proposal — confirm)*

## Sizes

| Size | Use | Text / status dot |
|---|---|---|
| 32 | Dense rows, tables, chips (default) | 14 px (body/medium) · 8 px |
| 40 | **List items** (M3 list avatar) | 16 px (body/large) · 10 px |
| 48 | Cards, headers | 20 px · 12 px |
| 64 | Profile summaries | 24 px (headline/small) · 16 px |
| 80 | Profile pages | 32 px (headline/large) · 20 px |
| 96 | Large profile / onboarding | 36 px (display/small) · 24 px |

The use per size (except 40 = list items) is a PDR proposal — confirm.

## Accessibility

- An avatar alone isn’t enough to identify a person — show the name next to it, or provide it as a tooltip / accessible label.
- The category icon is supported by text where the type matters (e.g. “Versicherung” in a caption).

## AI checklist

- [ ] Category matches the contact type
- [ ] Photo or Monogram for people; Bot / AI / Support for system actors
- [ ] Name shown next to the avatar
- [ ] Avatar group with overflow for teams

## Open questions for the team

- **Status:** what does `Show status` represent (presence, availability, employee status)?
- **Substitute avatar:** no uses in this file. Is it used in product files?
- **Category names:** German values (e.g. `Privatkunde`) — apply the same language rule as Status tags (English values, German labels)?

---

# Part 2 — Angular implementation

### API

```html
<pdr-avatar category="autohaus" [size]="40" [name]="customer.name" [src]="customer.photoUrl" />
<pdr-avatar category="ai" [size]="32" />
<pdr-avatar-group [users]="team" [max]="3" />
<pdr-substitute-avatar [person]="absent" [substitute]="deputy" />
```

| Figma | Input |
|---|---|
| Category (contact types) | `category="privatkunde | geschaeftskunde | autohaus | sachverstaendiger | rechtsanwalt | versicherung | leasing | fahrer"` → category icon + color |
| Category (system actors) | `category="support | bot | ai"` |
| Category=Photo / Monogram | `[src]` set → photo; no `src` → initials from `name` (automatic fallback, also when the image fails) |
| Category=Add new | `category="add"` — render inside a `<button>` with an `aria-label` (it is an action) |
| Category=Placeholder Phase 1 | `category="placeholder"` — only while data is missing |
| Size 32 · 40 · 48 · 64 · 80 · 96 | `[size]="32 | 40 | 48 | 64 | 80 | 96"` (default 32; **40 in list items**) |
| Show status | `[status]="…"` → status dot (8 / 10 / 12 / 16 / 20 / 24 px by size) — meaning still open (see Part 1) |
| Avatar group · Type | `<pdr-avatar-group>` — overlap, “+n” overflow chip when `users.length > max` |
| Substitute avatar | `<pdr-substitute-avatar>` (Vertretung) |

Text size inside monograms follows the spec’s Sizes table (body-medium at 32 → display-small at 96) — use the typography tokens, never pixel font sizes.

### Tokens

Shape `--mat-sys-corner-full`; category backgrounds `--pdr-sys-*-container` with text/icon `--pdr-sys-on-*-container` (one additional color per category — confirm the mapping with design); group overlap `-8px` with a 2 px `--mat-sys-surface` ring.

### A11y

Decorative avatar next to a visible name → `alt=""` / `aria-hidden="true"`; standalone avatar → `alt` / `aria-label` = person or company name (spec: an avatar alone never identifies a person).
