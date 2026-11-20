# Progress indicators

Figma page: **Progress indicators 🟢** `10808:999` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10808-999) · Figma Spec: [`10997:4480`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10997-4480)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Linear progress indicator`, `Circular progress indicator` · **Angular:** `<mat-progress-bar>`, `<mat-progress-spinner>` / `<mat-spinner>` · **Sources:** [M3 Progress indicators guidelines](https://m3.material.io/components/progress-indicators/guidelines), [M3 Loading indicator guidelines](https://m3.material.io/components/loading-indicator/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Progress indicators show the status of a process: how much is done (determinate) or that something is happening (indeterminate).

| Mode | Use |
|---|---|
| Determinate | Progress and wait time are known |
| Indeterminate | Progress and wait time are unknown |

**Don’t use** for page-level brand moments (login, app start, logout) → use the Brand loader (PDR). For content areas that are loading, prefer **Skeleton** placeholders (PDR).

## Anatomy

| # | Element | Notes |
|---|---|---|
| 1 | Active indicator | Shows progress |
| 2 | Track | Remaining part (linear) |
| 3 | Stop indicator | 4 px dot at the end of a **linear determinate** indicator (M3); not used for indeterminate or circular |

## Figma components and properties

| Component | Property | Values |
|---|---|---|
| Linear progress indicator | Mode | Determinate, Buffer, Indeterminate, Query |
| Linear progress indicator | Value | 0, 25, 50, 75, 100 (— for Indeterminate/Query) |
| Circular progress indicator | Mode | Determinate, Indeterminate |
| Circular progress indicator | Value | 25, 50, 75, 100 (— for Indeterminate) |
| Circular progress indicator | Size | 48, 24 |

## Decision rules

1. Progress is measurable → `Mode=Determinate`; the value **MUST** accurately represent the real progress.
2. Progress is unknown → `Mode=Indeterminate`.
3. When more information becomes available, **SHOULD** switch from indeterminate to determinate.
4. Linear → page-, section- or upload-level progress; stretches to any width.
5. Circular → compact or inline use. Inside buttons, use circular indicators for short, indeterminate activities under 5 seconds (`Size=24`).
6. Circular sizes MAY range from 24 to 240 px; this library offers 24 and 48.
7. In right-to-left languages, **MUST** mirror linear indicators; circular indicators aren’t mirrored.
8. `Mode=Buffer` / `Mode=Query` are Angular `mat-progress-bar` modes: Buffer for loading with a buffered part (e.g. streaming), Query before loading starts.

## Behavior and interaction

- Determinate indicators fill from 0 % to 100 %.
- Indeterminate indicators move along the track, growing and shrinking (animation exists only in code; Figma shows a still frame).
- Progress indicators aren’t interactive.

## States

No interaction states. Mode and value describe progress.

## Content guidelines

- Pair a determinate indicator with a short caption when the number helps (e.g. “3 of 4 photos”). *(PDR)*

## Usage guidelines

| Do | Don’t |
|---|---|
| Show real progress in determinate mode | Fake progress in a determinate indicator |
| Switch from indeterminate to determinate when possible | Use a progress indicator for the brand loader moments |
| Use circular 24 inside buttons and fields | Use circular indicators for long, measurable uploads |

## Accessibility

- The stop indicator on linear determinate indicators meets M3’s accessibility standard for showing the end of the track.

## AI checklist

- [ ] Determinate only when progress is measurable and accurate
- [ ] Linear for page/upload level, circular for inline
- [ ] Linear mirrored in RTL
- [ ] Skeleton for loading content areas, Brand loader for login / app start / logout

## Not covered by M3 (PDR conventions)

- **Stop indicator:** the Figma linear indicator has no stop indicator yet.
- **Track color:** the Figma components use `primary-container`. Check that this matches the Angular theme.
- **Loading indicator:** M3 also has a newer loading indicator (for 200 ms–5 s waits) that isn’t in this library or in Angular Material.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Linear Mode=X | `<mat-progress-bar mode="determinate|buffer|indeterminate|query" [value] [bufferValue]>` |
| Circular Mode=X | `<mat-progress-spinner mode="determinate|indeterminate" [value]>` |
| Size=48 / 24 | `[diameter]="48"` / `[diameter]="24"` (inside buttons: 18) |

Always label: `aria-label="Wird geladen"` or `aria-labelledby`. Full-page/branded loading → `../pdr/brand-loader.md`; content placeholders → `../pdr/skeleton-empty-error-states.md`.

### Overrides


None — Figma matches M3 defaults. Do not add any.
