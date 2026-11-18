# Summary modal

Figma: **Example/Summary modal** `10905:14849` · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10905-14849)
Dialog API: `../components/md3/dialogs.md`. Sample content: Task preview (`10905:14941`, mobile `9073:6450`).

## Structure
| Size | Container |
|---|---|
| Desktop (frame 1600) | scrim + **Dialog with scrollable content** 560 × ≤ 620 (`--pdr-dialog-width-l`), surface-container-lowest, `corner-extra-large`, level5 |
| Mobile (frame 375) | dialog full width (375), `corner-large` (`pdr-dialog--mobile`), max-height 620; switch to full-screen if content is longer |

Inside: `mat-dialog-title` · `mat-dialog-content` (scrolls; dividers appear on scroll) · `mat-dialog-actions align="end"`.

Summary rules: read-only definition lists (label-medium labels, body-medium values), status tag in the title row; actions limited to "Schließen" + one primary ("Öffnen", "Bearbeiten").

```ts
const mobile = this.bp.isMatched(PDR_BREAKPOINTS.mobile);
this.dialog.open(Component, {
  width: mobile ? '100vw' : 'var(--pdr-dialog-width-l)',
  maxWidth: mobile ? '100vw' : 'calc(100vw - 32px)',
  maxHeight: '620px',
  panelClass: ['pdr-dialog', ...(mobile ? ['pdr-dialog--mobile'] : [])],
});
```
