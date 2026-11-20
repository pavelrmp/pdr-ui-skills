# Timelines

Figma page: **Timelines 🟢** `3330:128` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-128) · Figma Spec: [`11038:3370`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11038-3370)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `History table`, `History row`, `History row simple`, `Row activity`, `Row`, `Date`, `Kundenkontakt` · **Angular:** custom PDR components (selectors to confirm) · **Sources:** components on this page; PDR Data Grids and Avatars rules

> **No M3 component.** Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Timelines show what happened to an order or customer over time — status changes, edits, customer contacts — newest first, grouped by date.

## Figma components and properties

| Component | Properties / use |
|---|---|
| History table | The full history list of an order |
| History row | State: Default, Hover · Size: Mobile — one history entry |
| History row simple | State: Default — compact entry |
| Row activity | Size: Widget, Changelog — activity entry for a widget or a changelog |
| Date | Date separator between days |
| Row | Generic row |
| Kundenkontakt | Customer contact entry (call, email, visit) |

## Decision rules

1. (PDR proposal — confirm) Newest entries first; group entries by day with `Date` separators.
2. (PDR proposal — confirm) Each entry shows who (Avatar with the right category), what, and when.
3. (PDR proposal — confirm) Use `History row` in the order history; `History row simple` where space is limited; `Row activity` in dashboard widgets and changelogs.
4. Status changes in the history use the Status tags colours.
5. Long histories follow the Data Grids rules for loading: skeleton rows while loading, “Load more” instead of pages on mobile.

## AI checklist

- [ ] Newest first, grouped by date
- [ ] Who · what · when in every entry
- [ ] Row variant by context
- [ ] Status colours from Status tags

## Open questions for the team

- **Naming:** `Kundenkontakt` is German and `Row` is generic. Rename (e.g. `Customer contact`, `Timeline row`) per the language rule.
- **States:** `History row simple` has only one variant; `History row` only a Mobile size. Add the missing sizes and states.
- **Deprecated layers:** `Kundenkontakt` still contains `Deprecated/…` layers.
- **Unused:** `History table` and `History row` have no uses in this file.

---

# Part 2 — Angular implementation

### API

```html
<pdr-timeline>
  <pdr-timeline-date [date]="day" />
  @for (e of events; track e.id) { <pdr-timeline-row [event]="e" size="widget|changelog" /> }
</pdr-timeline>
```
| Figma | Implementation |
|---|---|
| Row activity Widget / Changelog | `pdr-timeline-row size` — avatar + body-medium text + body-small time (on-surface-variant); vertical connector 1px `--mat-sys-outline-variant` |
| Date | sticky label-large separator |
| History row (+Hover) / simple / Mobile | `<pdr-history-row>` with state layer on hover; mobile stacks columns |
| History table | `mat-table` (see `../md3/data-grids.md`) |
| Kundenkontakt | `<pdr-contact-entry>` (channel icon + note) |

Semantics: `<ol>` list, times in `<time datetime>`.
