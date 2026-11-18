# WYSIWYG, Code, Drag-n-Drop

Figma page: **WYSIWYG, Code, Drag-n-Drop** `3330:129` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-129)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Drag and drop** `5649:28830` — `Status` Empty|Drag over|Uploading (start)|Uploading (complete)|Multiple files|Uploaded|Error|Disabled
- **WYSIWYG** `5649:29437`
- **Code editor** `5568:30914`

## Drag and drop → `<pdr-dropzone>`
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

## WYSIWYG → `<pdr-wysiwyg formControlName>`
Third-party editor wrapped as `ControlValueAccessor`; toolbar uses `matIconButton` + `mat-button-toggle-group`; container styled like outline `mat-form-field` (`--mat-sys-outline`, `corner-extra-small`). Output sanitized HTML.

## Code editor → `<pdr-code-editor [language] formControlName>`
Editor theme generated from tokens (background `--mat-sys-surface-container-low`, text `--mat-sys-on-surface`, keywords `--mat-sys-primary`, strings `--pdr-sys-success`, errors `--mat-sys-error`), monospace font.
