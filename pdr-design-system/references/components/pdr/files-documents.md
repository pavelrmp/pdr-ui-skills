# Files & Documents

Figma page: **Files & Documents** `9344:8816` · status 🌕 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=9344-8816)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

> 🌕 Not final in Figma. Use Material defaults / minimal styling and flag deviations in the PR.

## Components
- **Document card** `9362:5952`, **Documents** `10891:31572`
- **File icon/** CSV `9345:18370` · PNG `9345:18382` · JSON `9345:18391` · PDF `9345:18412` · File `10908:10280` · Chart `10908:10286`
- **Dropdown container** `10917:32916`, **ID container** `10917:32933`, **My view row** `10917:32969`

## Mapping
| Figma | Wrapper | Built from |
|---|---|---|
| Document card | `<pdr-document-card [file]>` | `mat-card appearance="outlined"` + `pdr-file-icon` + kebab `mat-menu` (Öffnen, Herunterladen, Löschen) |
| File icon/* | `<pdr-file-icon type="csv|png|json|pdf|chart|file">` | SVGs exported via MCP, `aria-hidden="true"` |
| Documents (list) | `<pdr-document-list>` | `mat-nav-list` or grid of cards; upload → `wysiwyg-code-dnd.md` dropzone |
| ID container | `<pdr-id-chip>` | copyable ID: `mat-chip` + `cdkCopyToClipboard` + snackbar |
| Dropdown container / My view row | `mat-select` / `mat-list-item` | see MD3 files |
