# Form sheet

Figma: **Example/Form sheet** `10911:18069` · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10911-18069)
Sheet API: `../components/md3/sheets.md`. Sample content: Edit Client (`10911:16274`).

## Structure
| Size | Container |
|---|---|
| Desktop (frame 1600) | scrim + **Side Sheet** 500 × full height, right edge, `surface-variant`, start corners `corner-large`, level3 |
| Mobile (frame 375) | full-screen (`pdr-dialog--fullscreen`) |

Anatomy: header (title-large + close `matIconButton`) · scrollable body (pad 16/24, sections 24 apart) · sticky action footer (actions right-aligned).

Use when the user edits an item while keeping the list visible. Form rules as in `form-modal.md`; saving closes the sheet and shows a snackbar.

```ts
this.dialog.open(Component, {
  position: { right: '0' }, width: '500px', height: '100dvh', maxWidth: '100vw',
  panelClass: ['pdr-dialog', 'pdr-side-sheet'],
});
```
