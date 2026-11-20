# Order preview

Figma page: **Order preview 🌕** `4546:19307` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=4546-19307) · Figma Spec: [`11037:5880`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11037-5880)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🌕 In progress · **Figma components:** 13 (see groups below) · **Angular:** custom PDR components (selectors to confirm) · **Sources:** components on this page; related PDR specs (Status tags, Avatars, Chats & Notes)

> **No M3 component.** Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Order preview shows an order — vehicle, customer, status and workshop progress — in compact forms: cards, popovers and chips, so people can see the essentials without opening the order.

## Component groups

| Group | Components | Use |
|---|---|---|
| **Order cards** | `Order card S` (Status: done, open, in repair), `Order card M`, `Order card v2` | An order in lists, boards and dashboards |
| **Order popover** | `Order popover` (Breakpoint: Deskop and Tablet, Mobile), `Order popover v1`, `Order popover v2` (Breakpoints: Tablet and Desktop, Mobile) | Quick preview of an order without leaving the page |
| **Order details** | `Order info`, `Replacement vehicle`, `Chat order info` | Blocks with order, vehicle and customer data (e.g. inside a popover or chat) |
| **Order links** | `Order link chip` (State: Enabled, Hovered), `Order not attached` (Order: Not attached, Attached) | Linking an item (document, chat) to an order |
| **Workshop progress** | `Workshop status` (Status: Default, Closed, Finish, Lack), `Workshop status compact` | Where the vehicle is in the repair process |

The former dashboard widgets (Orders overview, Today’s orders, Tasks, Announcements, Time clock, Sticky note …) and the recovered order parts (Car info, Order drawer, Stepper v1, Step icons …) are archived.

## Decision rules

1. Order status and workshop steps **MUST** use the Status tags rules (Process status / Repair status colours) — don’t create new colours.
2. People in orders use `Avatar` (Avatars) with the right category.
3. (PDR proposal — confirm) Lists and boards → `Order card S`; wide rows → `Order card M`; quick look without navigation → `Order popover`.
4. (PDR proposal — confirm) Link an item to an order with `Order link chip`; when no order is linked yet, show `Order not attached · Order=Not attached` with the “Auftrag zuordnen” action.
5. Multi-step flows use the **Stepper** component (Stepper page).

## AI checklist

- [ ] Status colours from Status tags
- [ ] Card size by context, popover for a quick look
- [ ] Links via Order link chip / Order not attached

## Open questions for the team — cleanup

- **Versions:** `Order card S / M / v2` and `Order popover / v1 / v2` — which version is current? Archive the others.
- **Typo:** `Order popover · Breakpoint=Deskop and Tablet` → “Desktop”. `Order popover v2` uses the property name “Breakpoints” — align both to “Breakpoint”.
- **Workshop status values:** `Lack` is German for paint (Lackvorbereitung). Use an English value (e.g. `Paint preparation`) per the language rule.
- **Deprecated layers:** `Order card M`, `Order card v2` and all three Order popovers still contain `Deprecated/Button`. Swap to the current Button.
- **Unused:** `Order card S/M/v2`, `Order popover v1/v2`, `Order info`, `Replacement vehicle`, `Order link chip`, `Order not attached` have no uses in this file.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Wrapper | Built from |
|---|---|---|
| Order card S / M / v2 | `<pdr-order-card [order] size="s|m">` | `mat-card appearance="outlined"`, `pdr-status-tag`, `pdr-avatar` |
| Status done/open/in repair | `pdr-status-tag` (success / info / warning) | see `status-tags.md` |
| Order popover (+Mobile) | `<pdr-order-popover>` | desktop: `cdkConnectedOverlay` (surface-container-lowest, `corner-large`, level3); mobile: `MatBottomSheet` |
| Workshop status (+compact) | `<pdr-workshop-status [status] [compact]>` | `pdr-process-status` + `mat-progress-bar` |
| Order link chip | `<pdr-order-link-chip>` | `mat-chip` + `routerLink` |
| Order not attached | `<pdr-order-attach>` | outlined `matButton` "Auftrag zuordnen" / attached `pdr-order-link-chip` |
| Car info / Order customer info / Order info | `<pdr-car-info>`, `<pdr-customer-info>`, `<pdr-order-info>` | definition lists (`dl`), label-medium labels + body-medium values |
| Replacement vehicle | `<pdr-replacement-vehicle>` | `mat-card` |
| Employee row | `<pdr-employee-row>` | `mat-list-item` + `pdr-avatar` + `pdr-employee-status` |
| Stepper v1 | `pdr-wizard-steps` | see `workflows.md` |
| Order preview toolbar | `<pdr-order-toolbar>` | see `toolbars-pdr.md` |
