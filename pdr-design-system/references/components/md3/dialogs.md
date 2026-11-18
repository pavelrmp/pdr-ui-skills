# Dialogs

Figma page: **Dialogs** `3330:117` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-117)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

Widths come from Figma collection **Modals**. Always open via `MatDialog`; always set `panelClass`.

## Components

Use: `Basic dialog` `10905:17519`, `Dialog with scrollable content` `10905:17533`, `Dialog title and description` `10905:17500`, `Dialog actions` `10905:17546`, `Full-screen dialog header` `7181:10816`, `Dialog toolbar` `10917:39470`. Ignore all `Deprecated/*`.

Figma surface: `<Paper>` = surface-container-lowest, `corner-extra-large` (28) desktop / `corner-large` (16) mobile, level5.

### Widths (Figma `Modals`)

| Token | px | Typical use |
|---|---|---|
| `--pdr-dialog-width-s` | 280 | confirm, mobile basic |
| `--pdr-dialog-width-m` | 420 | basic dialog (default) |
| `--pdr-dialog-width-l` | 560 | short form |
| `--pdr-dialog-width-xl` | 900 | scrollable content, tables |
| `--pdr-dialog-width-xxl` | 1200 | editors |
| `--pdr-dialog-width-xxxl` | 1536 | full workspace |

### Opening

```ts
private dialog = inject(MatDialog);

openConfirm() {
  return this.dialog.open(ConfirmDialog, {
    width: 'var(--pdr-dialog-width-m)',
    maxWidth: 'calc(100vw - 32px)',
    panelClass: 'pdr-dialog',
    autoFocus: 'first-tabbable',
    data: { title: 'Auftrag löschen?' },
  });
}

openFullscreen() {   // Figma Full-screen dialog header / mobile
  return this.dialog.open(EditOrderDialog, {
    width: '100vw', height: '100dvh', maxWidth: '100vw',
    panelClass: ['pdr-dialog', 'pdr-dialog--fullscreen'],
  });
}
```
On viewports below the `M` breakpoint (768px), add `pdr-dialog--mobile` via `BreakpointObserver`.

### Template mapping

| Figma part | Angular |
|---|---|
| Dialog title (`Vertical` True→ icon above title) | `<h2 mat-dialog-title>`; icon variant → `<mat-icon class="pdr-dialog__icon">` before it + `class="pdr-dialog__title--center"` on the title |
| Dialog title and description | `<h2 mat-dialog-title>` + first `<p>` in content (body-medium, on-surface-variant) |
| Dialog content / scrollable content | `<mat-dialog-content>` (scrolls natively; dividers appear on scroll) |
| Dialog actions: 1 / 2 / 3 buttons | `<mat-dialog-actions align="end">` with text / filled `matButton`; primary action last |
| Dialog actions: delete + 3 buttons | destructive `matButton class="pdr-btn--error"` first + `<span class="pdr-spacer">` then the rest |
| Dialog actions: with a comment | `mat-form-field` in content above actions |
| Dialog toolbar | `<pdr-dialog-toolbar [title]>` (`matIconButton` close + actions) |
| Full-screen dialog header | `<pdr-dialog-toolbar variant="fullscreen">` (close left, save `matButton` right) |

```html
<h2 mat-dialog-title>Auftrag löschen?</h2>
<mat-dialog-content>Dieser Schritt kann nicht rückgängig gemacht werden.</mat-dialog-content>
<mat-dialog-actions align="end">
  <button matButton mat-dialog-close>Abbrechen</button>
  <button matButton="filled" class="pdr-btn--error" [mat-dialog-close]="true" cdkFocusInitial>Löschen</button>
</mat-dialog-actions>
```

## Overrides (`styles/components/md3/_dialogs.scss`)

```scss
@use '@angular/material' as mat;

html {
  // Figma <Paper>: surface-container-lowest + level5 (M3: surface-container-high, no shadow)
  @include mat.dialog-overrides((
    container-color: var(--mat-sys-surface-container-lowest),
    container-elevation-shadow: var(--mat-sys-level5),
  ));
}
.pdr-dialog--mobile     { @include mat.dialog-overrides((container-shape: var(--mat-sys-corner-large))); }
.pdr-dialog--fullscreen { @include mat.dialog-overrides((container-shape: 0, container-elevation-shadow: none)); }
.pdr-dialog__title--center { text-align: center; }
.pdr-spacer { flex: 1 1 auto; }
```
