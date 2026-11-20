# Examples (Figma page "Examples")

Figma page: **Examples** `10723:10427` · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10723-10427)

Examples are full-page compositions. Start every new screen from the closest example, then fill it with components from `../components/`. Examples define **layout, regions and spacing**; components define everything inside.

| Example | File | Figma | Use for |
|---|---|---|---|
| App shell | `app-shell.md` | `10723:15611` | Every authenticated page (base for all others) |
| Data grid page | `data-grid-page.md` | `10723:14870` | List/overview pages (orders, tasks, invoices) |
| Settings page | `settings-page.md` | `10724:30020` | Settings, profile, admin configuration |
| Filters | `filters.md` | `10798:15767` | Filter bars above lists/analytics |
| Full-screen modal shell | `fullscreen-modal-shell.md` | `10724:34607` | Large create/edit flows with tabs (order, client) |
| Form modal | `form-modal.md` | `10905:20089` | Short create/edit forms in a dialog |
| Summary modal | `summary-modal.md` | `10905:14849` | Read-only preview in a dialog |
| Form sheet | `form-sheet.md` | `10911:18069` | Edit next to the list (side sheet) |
| Summary sheet | `summary-sheet.md` | `10908:11536` | Preview next to the list (side sheet) |
| Calendars 🌕 | `calendars.md` | `11008:46064` (spec) | Workshop planning views: appointments, Gantt bars, vehicles in workshop |

Sample contents used inside the shells: Incoming order (`5743:19955`, mobile `10908:11375`), Payment details (`10905:19292`), Edit Client (`10911:16274`), Task preview (`10905:14941`, mobile `9073:6450`).

## Modal vs sheet vs full-screen
- **Sheet** when the user needs the list in view (compare, step to the next item). Width 500.
- **Modal** for a focused task that blocks the page; width from `Modals` (L 560 for forms).
- **Full-screen modal** for multi-section flows (tabs) or anything taller than ~2 screens.
- On mobile (< 768 px) all three become full-screen.
