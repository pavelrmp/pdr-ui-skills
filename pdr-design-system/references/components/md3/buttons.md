# Buttons

Figma page: **Buttons** `3330:88` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-88)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

Color modes come from Figma collection **Button color** (Primary | Error | Success). Segmented buttons: see `button-toggle.md`.

## Button — `10007:3190`

Props: `Size` Large|Medium|Small · `Style` Filled|Outlined|Text|Tonal|Elevated · `State` Enabled|Hovered|Focused|Pressed|Loading|Disabled

| Figma | Angular |
|---|---|
| Style=Filled | `<button matButton="filled">` |
| Style=Tonal | `<button matButton="tonal">` |
| Style=Outlined | `<button matButton="outlined">` |
| Style=Text | `<button matButton>` |
| Style=Elevated | `<button matButton="elevated">` (tokens prefixed `protected-*`) |
| Size=Medium (40px) | default |
| Size=Small (32px) / Large (48px) | `class="pdr-btn--sm"` / `class="pdr-btn--lg"` |
| State=Disabled | `[disabled]="true"` (use `disabledInteractive` if it needs a tooltip) |
| State=Loading | `<pdr-button [loading]="saving">` |
| Hovered / Focused / Pressed | native, never coded |
| Button color = Error / Success | `class="pdr-btn--error"` / `class="pdr-btn--success"` |
| Leading icon | `<mat-icon fontSet="material-symbols-outlined">add</mat-icon>` as first child (icon spacing 8px) |

Do **not** use `color="primary|accent|warn"`. It needs the M2 back-compat mixin and does not cover Success.

```html
<button matButton="filled">Speichern</button>
<button matButton="tonal" class="pdr-btn--sm"><mat-icon fontSet="material-symbols-outlined">add</mat-icon>Neu</button>
<button matButton="outlined" class="pdr-btn--error">Löschen</button>
<a matButton routerLink="/orders">Alle Aufträge</a>
```

### `pdr-button` (loading wrapper)

```ts
@Component({
  selector: 'pdr-button',
  template: `
    <button [matButton]="appearance()" [disabled]="disabled() || loading()" [attr.aria-busy]="loading()" [class]="sizeClass()">
      @if (loading()) { <mat-progress-spinner mode="indeterminate" diameter="18" /> }
      <ng-content />
    </button>`,
  imports: [MatButton, MatProgressSpinner],
})
export class PdrButton {
  appearance = input<'filled' | 'tonal' | 'outlined' | 'elevated' | 'text'>('filled');
  size = input<'sm' | 'md' | 'lg'>('md');
  loading = input(false);
  disabled = input(false);
  sizeClass = computed(() => (this.size() === 'md' ? '' : `pdr-btn--${this.size()}`));
}
```

## Icon button — `10007:3136`

Props: `Size` Small|Medium|Large · `Style` Filled|Outlined|Text|Tonal|Elevated · `State` …|Loading

| Figma | Angular |
|---|---|
| Style=Text | `<button matIconButton aria-label="…">` (default) |
| Style=Filled / Tonal / Outlined / Elevated | `matIconButton` + `class="pdr-icon-btn--filled|--tonal|--outlined|--elevated"` |
| Size=Small 32 / Medium 40 / Large 48 | `pdr-icon-btn--sm` / default / `pdr-icon-btn--lg` |

`aria-label` is mandatory. Icon color default = `on-surface-variant` (Figma `icon-standard/content`).

## FAB — `4157:32313`

Props: `Style` Primary|Secondary|Outlined · 56×56, `corner-large`, level3

| Figma | Angular |
|---|---|
| Style=Secondary | `<button matFab>` (M3 default = primary-container) |
| Style=Primary | `<button matFab class="pdr-fab--primary">` |
| Style=Outlined | `<button matFab class="pdr-fab--surface">` |
| Extended (label) | `<button matFab extended>` |

## Overrides (`styles/components/md3/_buttons.scss`)

```scss
@use '@angular/material' as mat;

html {
  // Figma: tonal = primary-container (M3: secondary-container); horizontal padding 16 (M3: 24)
  @include mat.button-overrides((
    tonal-container-color: var(--mat-sys-primary-container),
    tonal-label-text-color: var(--mat-sys-on-primary-container),
    tonal-state-layer-color: var(--mat-sys-on-primary-container),
    filled-horizontal-padding: 16px, tonal-horizontal-padding: 16px,
    outlined-horizontal-padding: 16px, protected-horizontal-padding: 16px,
  ));
}

// Sizes (Figma Size=Small|Large)
@each $size, $h in (sm: 32px, lg: 48px) {
  .pdr-btn--#{$size} {
    @include mat.button-overrides((
      filled-container-height: $h, tonal-container-height: $h, outlined-container-height: $h,
      protected-container-height: $h, text-container-height: $h,
    ));
  }
  .pdr-icon-btn--#{$size} { @include mat.icon-button-overrides((state-layer-size: $h)); }
}

// Color modes (Figma collection 'Button color')
$modes: (
  error:   (var(--mat-sys-error),   var(--mat-sys-on-error),   var(--mat-sys-error-container),   var(--mat-sys-on-error-container)),
  success: (var(--pdr-sys-success), var(--pdr-sys-on-success), var(--pdr-sys-success-container), var(--pdr-sys-on-success-container)),
);
@each $name, $c in $modes {
  .pdr-btn--#{$name} {
    @include mat.button-overrides((
      filled-container-color: nth($c, 1), filled-label-text-color: nth($c, 2), filled-state-layer-color: nth($c, 2),
      tonal-container-color: nth($c, 3), tonal-label-text-color: nth($c, 4), tonal-state-layer-color: nth($c, 4),
      text-label-text-color: nth($c, 1), text-state-layer-color: nth($c, 1),
      outlined-label-text-color: nth($c, 1), outlined-state-layer-color: nth($c, 1),
    ));
  }
}

// Icon button appearances (Figma Icon button Style) (no native filled/tonal icon button yet)
.pdr-icon-btn--filled   { background: var(--mat-sys-primary); @include mat.icon-button-overrides((icon-color: var(--mat-sys-on-primary), state-layer-color: var(--mat-sys-on-primary))); }
.pdr-icon-btn--tonal    { background: var(--mat-sys-primary-container); @include mat.icon-button-overrides((icon-color: var(--mat-sys-on-primary-container), state-layer-color: var(--mat-sys-on-primary-container))); }
.pdr-icon-btn--outlined { box-shadow: inset 0 0 0 1px var(--mat-sys-outline); }
.pdr-icon-btn--elevated { background: var(--mat-sys-surface-container-low); box-shadow: var(--mat-sys-level1); }

// FAB (Figma Style=Primary | Outlined)
.pdr-fab--primary { @include mat.fab-overrides((container-color: var(--mat-sys-primary), foreground-color: var(--mat-sys-on-primary), state-layer-color: var(--mat-sys-on-primary))); }
.pdr-fab--surface { @include mat.fab-overrides((container-color: var(--mat-sys-surface-container-lowest), foreground-color: var(--mat-sys-primary))); }
```
