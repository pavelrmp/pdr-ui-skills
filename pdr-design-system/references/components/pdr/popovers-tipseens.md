# Popovers & Tipseens

Figma page: **Popovers & Tipseens 🟢** `3330:123` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-123) · Figma Spec: [`11037:9793`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11037-9793)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Onboarding tipseen`, `Walkthrough tipseen`, `Onboarding modal`, `Onboarding modal v1`, `Welcome illustration`, `Module popover`, `Video player`, `Video frame` · **Angular:** custom PDR components (selectors to confirm) · **Sources:** component descriptions on this page; [M3 Tooltips](https://m3.material.io/components/tooltips/guidelines) and [M3 Dialogs](https://m3.material.io/components/dialogs/guidelines) for the neighbouring patterns

> **No M3 component.** Tipseens are a PDR onboarding pattern. Rules from the component descriptions are binding; others are marked **(PDR proposal — confirm)**.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Tipseens are a “virtual unboxing experience” that helps people get started with the system and discover new features. They give additional context about new UI elements.

| Need | Use |
|---|---|
| Point at one new UI element | `Onboarding tipseen` (Alignment: on bottom, on top) |
| Guide through several new features in sequence | `Walkthrough tipseen` |
| Welcome people or introduce a larger change | `Onboarding modal` (Size: Mobile, Tablet and desktop) with `Welcome illustration` or `Video player` |
| Short label for an icon button | Tooltip (M3) — not a tipseen |
| Information about a module / feature on demand | `Module popover` |

## Figma components and properties

| Component | Properties |
|---|---|
| Onboarding tipseen | Alignment: on bottom, on top |
| Onboarding modal | Size: Mobile, Tablet and desktop |
| Walkthrough tipseen · Onboarding modal v1 · Welcome illustration · Module popover · Video player · Video frame | No properties |

## Decision rules

1. Use tipseens for onboarding screens, new-feature discovery or any guidance people need — when they aren’t yet familiar with the UI or are ready to learn about it. *(from the component descriptions)*
2. Tipseens appear when the page is loaded for the first time. *(from the descriptions)*
3. A tipseen stays until it’s closed with the **X** button or its call-to-action button. *(from the descriptions)*
4. Tipseens MAY include a subheading, buttons and hyperlinks. *(from the descriptions)*
5. (PDR proposal — confirm) Choose `Alignment` so the tipseen points at its element without covering it (`on bottom` below the element, `on top` above it).
6. (PDR proposal — confirm) Show only one tipseen at a time; a walkthrough shows its steps one after another.
7. (PDR proposal — confirm) Don’t show tipseens again once closed.

## AI checklist

- [ ] Tipseen only for onboarding or new features, on first load
- [ ] Closable with X or a call to action
- [ ] One tipseen at a time; tooltips for simple icon labels
- [ ] Onboarding modal for welcome or larger changes

## Open questions for the team

- **Versions:** `Onboarding modal` vs `Onboarding modal v1` — which is current?
- **Unused:** all components except `Welcome illustration` have no uses in this file.
- **Deprecated layers:** `Walkthrough tipseen` and `Module popover` still contain `Deprecated/…` layers.
- **Video:** when is `Video player` used (onboarding modal, help)?

---

# Part 2 — Angular implementation

### Mapping

| Figma | Wrapper | Built from |
|---|---|---|
| Onboarding / Walkthrough tipseen | `<pdr-tipseen [anchor] position="below|above" [step] [total]>` | `cdkConnectedOverlay` (inverse-surface or primary per Figma, `corner-medium`, level2, arrow), `matButton` "Weiter"/"Überspringen" |
| Onboarding modal (+Mobile) | `MatDialog` with `panelClass: ['pdr-dialog','pdr-onboarding']`, width `--pdr-dialog-width-l`; mobile full-screen | see `../md3/dialogs.md` |
| Module popover | `<pdr-module-popover>` | `cdkConnectedOverlay`, surface-container-lowest, `corner-large`, level3 |
| Video frame / player | `<pdr-video-player [src]>` | native `<video controls>` + captions track |

Tipseen: focus moves into the tipseen, Esc closes, completion persisted per user.
