# Calendars

Figma page: **Examples** `10723:10427` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10723-10427) · Figma Spec: [`11008:46064`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11008-46064)
Tokens: `../tokens/`. Components: `../components/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🌕 In progress · **Figma components:** `Calendar header full-screen`, `Calendar header full-screen mobile`, `Gantt bar`, `Vehicle in workshop`; reference frames “Calendars”, “Calendars mobile”, “Calendar grids examples” · **Angular:** custom PDR components (selectors to confirm) · **Sources:** components and frames on this page; [M3 Date pickers](https://m3.material.io/components/date-pickers/guidelines) for date selection

> **No M3 component.** M3 covers date *selection* (date pickers), not planning calendars. Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Calendars show workshop planning over time — appointments, vehicles in the workshop and repair durations — so people can plan capacity and see what happens when.

| Need | Use |
|---|---|
| Pick a date or range in a form | Datepickers (MD3 page) |
| Plan and view appointments and repairs over days or weeks | **Calendars** |

## Figma components and properties

| Component | Properties / use |
|---|---|
| Calendar header full-screen | Desktop header (1128 px): calendar label, “Heute” (today), period (e.g. “10 Feb. — 22 Feb.”), view switch (“Woche”), branch filter (“Alle Filialen”) |
| Calendar header full-screen mobile | The same for mobile |
| Gantt bar | Property 1: Default, small — a duration bar on the timeline with its duration (e.g. “2h 55m”) |
| Vehicle in workshop | Small indicator (59 × 32 px) marking that a vehicle is in the workshop |

## Decision rules

1. Desktop and tablet use `Calendar header full-screen`; mobile uses `Calendar header full-screen mobile`.
2. Use `Gantt bar` for anything with a start and end on the timeline; `small` in dense rows. *(PDR proposal — confirm)*
3. Use the “Calendar grids examples” frame as the reference for day / week layouts until grid components exist.
4. Appointment types use the **Appointment** status tags (Status tags page) with their fixed colours.
5. To pick a single date or range, use the Datepickers — not the planning calendar.

## AI checklist

- [ ] Planning view → Calendars; date input → Datepickers
- [ ] Header variant by screen size
- [ ] Durations as Gantt bars
- [ ] Appointment colours from the Appointment status tags

## Open questions for the team

- **Incomplete components:** `Gantt bar` and `Vehicle in workshop` were recovered from an old library. `Gantt bar` still uses a default “Property 1” property. Name the property (e.g. Size) and add the missing states and colours.
- **Calendar grid components:** day / week / month grids exist only as example frames. Should they become components?
- **Headers:** the two calendar headers have no properties and no uses in this file. Define the view switch (day / week / month) and the date navigation as properties.
- **Status:** the page is 🌕. What is missing to make it 🟢?

---

# Part 2 — Angular implementation

### Mapping

| Figma | Wrapper | Built from |
|---|---|---|
| Calendar header full-screen | `<pdr-calendar-header [view] [date]>` | `matIconButton` prev/next, `mat-button-toggle-group` (Tag/Woche/Monat), `matButton` "Heute" |
| Gantt bar | `<pdr-gantt-bar [start] [end] [status] size="default|small">` | absolutely positioned within planner grid; color from status → `--pdr-sys-*-container` |
| Vehicle in workshop | `<pdr-workshop-vehicle>` | `pdr-avatar` / car thumbnail + body-medium |

Planner grid columns reuse Data Grids column headers `Col Week / Col Day / Col Range` (`../components/md3/data-grids.md`). Drag to reschedule → `cdkDrag` with `cdkDragLockAxis="x"`.
