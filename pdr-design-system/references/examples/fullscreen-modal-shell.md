# Full-screen modal shell

Figma: **Example/Full-screen modal shell** `10724:34607` · `Breakpoint` Desktop | Tablet | Mobile · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10724-34607)
Dialog API: `../components/md3/dialogs.md`.

## Structure (all breakpoints)
```
surface-container-lowest (full viewport)
├── Full-screen dialog header   64 px, pad 8/16 — close (left) · title · primary action (right)
├── Tabs                        49 px, pad 0/24 (0/16 mobile), outline-variant divider
└── Scrollable content          sections in panels / form groups, max-width 1128, centered
```
Sample contents: Edit Client (`10911:16274`), Incoming order (`5743:19955`).

## Angular
```ts
this.dialog.open(EditClientDialog, {
  width: '100vw', height: '100dvh', maxWidth: '100vw',
  panelClass: ['pdr-dialog', 'pdr-dialog--fullscreen'],
  autoFocus: 'first-tabbable',
});
```
```html
<pdr-dialog-toolbar variant="fullscreen" title="Kunde bearbeiten" (close)="close()">
  <button matButton="filled" pdrDialogAction (click)="save()" [disabled]="form.invalid">Speichern</button>
</pdr-dialog-toolbar>
<mat-tab-group mat-stretch-tabs="false">
  <mat-tab label="Stammdaten">…</mat-tab>
  <mat-tab label="Fahrzeuge">…</mat-tab>
</mat-tab-group>
```
## Rules
- Header and tabs stay fixed; only tab content scrolls.
- Closing with unsaved changes asks for confirmation (small dialog, `--pdr-dialog-width-s`).
