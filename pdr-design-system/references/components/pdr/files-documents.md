# Files & Documents

Figma page: **Files & Documents 🌕** `9344:8816` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=9344-8816) · Figma Spec: [`11036:8508`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11036-8508)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🌕 In progress · **Figma components:** `Documents` (document tile), `Document missing`, `Document card`, `File icon/PDF · PNG · CSV · JSON · Chart · File`, `My view row` · **Angular:** custom PDR components (selectors to confirm) · **Sources:** components on this page

> **No M3 component.** Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Files & Documents show the documents attached to an order — invoices, cost approvals, service agreements, inspection reports — and which required documents are still missing.

## Figma components and properties

| Component | Use |
|---|---|
| Documents | A document tile (170 × 114) with file name, e.g. “Leistungsvereinbarung.pdf” |
| Document missing | Placeholder tile (170 × 114) for a document that is expected but not uploaded, e.g. “TÜV (optional)” |
| Document card | A card listing an order’s documents (e.g. Leistungsvereinbarung, RKÜ-Bestätigung, Reparaturrechnung) |
| File icon/… | 24 px file-type icons: PDF, PNG, CSV, JSON, Chart, File (generic) |
| My view row | Row of a saved “my view” list (recovered; State=Default) |

## Decision rules

1. **MUST** use the file icon that matches the file type; unknown types → `File icon/File`.
2. Show expected but missing documents with `Document missing` in the same grid as the uploaded ones, so gaps are visible. *(PDR proposal — confirm)*
3. Mark optional documents in the label (“(optional)”), as in `Document missing`.
4. (PDR proposal — confirm) Use `Document card` to show all documents of one order; use `Documents` tiles inside it or in a grid.
5. File names show the full name with extension; truncate in the middle only if needed. *(PDR proposal — confirm)*

## AI checklist

- [ ] File icon matches the file type
- [ ] Missing documents shown as placeholders, optional ones marked
- [ ] Documents grouped per order

## Open questions for the team

- **Deprecated layers:** `Documents`, `Document missing`, `Document card` and `My view row` still contain `Deprecated/Button`. Swap to the current Button.
- **States:** `Documents` and `Document missing` have no properties (no hover, selected, uploading or error states). Which states exist in code?
- **Uploading:** how are upload progress and failed uploads shown? (Linear progress?)
- **`My view row`:** recovered with a default property and placed on this page. Does it belong to Files & Documents?
- **Unused components:** `Document card`, `Document missing`, `File icon/File` and `File icon/Chart` have no uses in this file.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Wrapper | Built from |
|---|---|---|
| Document card | `<pdr-document-card [file]>` | `mat-card appearance="outlined"` + `pdr-file-icon` + kebab `mat-menu` (Öffnen, Herunterladen, Löschen) |
| File icon/* | `<pdr-file-icon type="csv|png|json|pdf|chart|file">` | SVGs exported via MCP, `aria-hidden="true"` |
| Documents (list) | `<pdr-document-list>` | `mat-nav-list` or grid of cards; upload → `wysiwyg-code-dnd.md` dropzone |
| ID container | `<pdr-id-chip>` | copyable ID: `mat-chip` + `cdkCopyToClipboard` + snackbar |
| Dropdown container / My view row | `mat-select` / `mat-list-item` | see MD3 files |
