# WYSIWYG, Code, Drag-n-Drop

Figma page: **WYSIWYG, Code, Drag-n-Drop 🟢** `3330:129` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-129) · Figma Spec: [`11038:4015`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11038-4015)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Drag and drop`, `WYSIWYG`, `Code editor` · **Angular:** custom PDR components / third-party editors (selectors to confirm) · **Sources:** components on this page; MD3 Progress indicators and Form fields specs

> **No M3 component.** Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

| Component | Use |
|---|---|
| Drag and drop | Upload files by clicking or dragging them in (e.g. bank statements “Kontoauszug.pdf”) |
| WYSIWYG | Formatted text input (font, size, headings) for longer descriptions |
| Code editor | Editing code snippets, e.g. an embedded widget (`<iframe>`), with line numbers |

## Figma components and properties

| Component | Properties |
|---|---|
| Drag and drop | Status: Empty, Drag over, Uploading (start), Uploading (complete), Multiple files, Uploaded, Error, Disabled |
| WYSIWYG · Code editor | No properties |

## Drag and drop — states

| Status | Shows |
|---|---|
| Empty | “Klicke zum Hochladen oder ziehe deine …” — click or drag to upload |
| Drag over | Same text, highlighted drop area while a file is dragged over it |
| Uploading (start) / (complete) | File name, size and progress (e.g. 1 % → 99 %) |
| Multiple files | Several files with their own progress |
| Uploaded | File name and size |
| Error | File name and “Upload fehlgeschlagen” |
| Disabled | Upload not available |

## Decision rules

1. Use `Drag and drop` whenever people upload files; it always offers **click to upload** as well as dragging (keyboard and touch users can’t drag).
2. Show progress per file while uploading (determinate, as in Linear progress); show each file separately for multiple uploads.
3. On `Error`, keep the file in the list with “Upload fehlgeschlagen” and offer to retry. *(PDR proposal — confirm: retry action)*
4. (PDR proposal — confirm) State accepted file types and the maximum size in the empty state.
5. Use `WYSIWYG` only where formatting is needed; plain multi-line text uses the **Text area** (Input page).
6. Use `Code editor` only for technical content (embed codes, templates), not for normal text.

## AI checklist

- [ ] Click to upload + drag and drop
- [ ] Progress per file, errors kept visible
- [ ] Text area for plain text, WYSIWYG only for formatting
- [ ] Code editor only for code

## Open questions for the team

- **WYSIWYG / Code editor:** which editor libraries are used in Angular? They have no properties (toolbar options, read-only, error).
- **Deprecated layers:** `Drag and drop` (10 layers) and `WYSIWYG` (3) still contain `Deprecated/…` layers.

---

# Part 2 — Angular implementation

### Drag and drop → `<pdr-dropzone>`

```html
<pdr-dropzone accept=".pdf,.png,.jpg" [multiple]="true" [maxSizeMb]="20" (files)="upload($event)" />
```
| Figma Status | Implementation |
|---|---|
| Empty | dashed 1px `--mat-sys-outline`, `corner-medium`, icon + body-medium + `matButton="outlined"` "Datei auswählen" (hidden `<input type="file">`) |
| Drag over | border `--mat-sys-primary`, bg `--mat-sys-primary-container` |
| Uploading start / complete | per file `mat-progress-bar mode="determinate"` + `pdr-file-icon` |
| Multiple files / Uploaded | file list with remove `matIconButton` |
| Error | `--mat-sys-error` border + `<mat-error>`-style message |
| Disabled | `--pdr-sys-on-surface-disabled`, `aria-disabled` |
Drop zone must also be keyboard-operable (Enter/Space opens file dialog).

### WYSIWYG → `<pdr-wysiwyg formControlName>`

Third-party editor wrapped as `ControlValueAccessor`; toolbar uses `matIconButton` + `mat-button-toggle-group`; container styled like outline `mat-form-field` (`--mat-sys-outline`, `corner-extra-small`). Output sanitized HTML.

### Code editor → `<pdr-code-editor [language] formControlName>`

Editor theme generated from tokens (background `--mat-sys-surface-container-low`, text `--mat-sys-on-surface`, keywords `--mat-sys-primary`, strings `--pdr-sys-success`, errors `--mat-sys-error`), monospace font.
