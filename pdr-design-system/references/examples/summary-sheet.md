# Summary sheet

Figma: **Example/Summary sheet** `10908:11536` · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10908-11536)
Sheet API: `../components/md3/sheets.md`. Sample content: Incoming order (`5743:19955`, mobile `10908:11375`).

## Structure
| Size | Container |
|---|---|
| Desktop (frame 1600) | scrim + **Side Sheet** 500 × full height, right edge, `surface-variant`, start corners `corner-large`, level3 |
| Mobile (frame 375) | full-screen (`pdr-dialog--fullscreen`) |

Anatomy: header (title-large + close `matIconButton`) · scrollable body (pad 16/24, sections 24 apart) · sticky action footer (actions right-aligned).

Use for a quick preview from a list row (row click on desktop). Previous/next arrow buttons (`pdr-icon-btn--outlined`) in the header may step through the list.

```ts
this.dialog.open(Component, {
  position: { right: '0' }, width: '500px', height: '100dvh', maxWidth: '100vw',
  panelClass: ['pdr-dialog', 'pdr-side-sheet'],
});
```
