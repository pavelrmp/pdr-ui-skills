# Form modal

Figma: **Example/Form modal** `10905:20089` · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10905-20089)
Dialog API: `../components/md3/dialogs.md`. Sample content: Payment details (`10905:19292`).

## Structure
| Size | Container |
|---|---|
| Desktop (frame 1600) | scrim + **Dialog with scrollable content** 560 × ≤ 620 (`--pdr-dialog-width-l`), surface-container-lowest, `corner-extra-large`, level5 |
| Mobile (frame 375) | dialog full width (375), `corner-large` (`pdr-dialog--mobile`), max-height 620; switch to full-screen if content is longer |

Inside: `mat-dialog-title` · `mat-dialog-content` (scrolls; dividers appear on scroll) · `mat-dialog-actions align="end"`.

Form rules: fields `appearance="outline"`, single column, labels via `mat-label`, primary action `matButton="filled"` last; validate on blur and on submit. Use when the form fits in ~1.5 screens; otherwise use `fullscreen-modal-shell.md` or `form-sheet.md`.

```ts
const mobile = this.bp.isMatched(PDR_BREAKPOINTS.mobile);
this.dialog.open(Component, {
  width: mobile ? '100vw' : 'var(--pdr-dialog-width-l)',
  maxWidth: mobile ? '100vw' : 'calc(100vw - 32px)',
  maxHeight: '620px',
  panelClass: ['pdr-dialog', ...(mobile ? ['pdr-dialog--mobile'] : [])],
});
```
