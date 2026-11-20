# Buttons

Figma page: **Buttons 🟢** `3330:88` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-88) · Figma Spec: [`10993:1587`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10993-1587)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Button`, `Icon button`, `FAB` · **Angular:** Material buttons (`matButton` filled / outlined / text / tonal / elevated), `mat-icon-button`, `mat-fab` · **Sources:** [All buttons](https://m3.material.io/components/all-buttons), [Buttons guidelines](https://m3.material.io/components/buttons/guidelines), [Icon buttons](https://m3.material.io/components/icon-buttons/guidelines), [Icon button accessibility](https://m3.material.io/components/icon-buttons/accessibility), [FAB accessibility](https://m3.material.io/components/floating-action-button/accessibility), [Extended FAB](https://m3.material.io/components/extended-fab/guidelines)

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

Buttons let people take action and make choices with one tap.

| Component | Use for |
|---|---|
| Button | A labelled action |
| Icon button | A minor action whose icon is unambiguous (e.g. favourite, download, more) |
| FAB | The single most important action on a screen |

**Don’t use a button** to select options (use segmented buttons, chips, radio buttons or checkboxes) or to navigate between top-level destinations (use navigation components).

## Anatomy

| Component | Elements |
|---|---|
| Button | Container (none for Text) · Label text · Leading icon (optional) · Trailing icon (optional) |
| Icon button | Container (none for Text/standard) · Icon |
| FAB | Container · Icon |

## Figma components and properties

| Component | Property | Values |
|---|---|---|
| Button | Style | Filled, Tonal, Elevated, Outlined, Text |
| Button | Size | Small, Medium, Large |
| Button | State | Enabled, Hovered, Focused, Pressed, Loading, Disabled |
| Button | Label text · Show leading icon · Leading icon name · Show trailing icon · Trailing icon name | Text / toggles |
| Icon button | Style | Filled, Tonal, Elevated, Outlined, Text (= M3 “standard”) |
| Icon button | Size | Small, Medium, Large |
| Icon button | State | Enabled, Hovered, Focused, Pressed, Loading, Disabled |
| Icon button | Icon name | Material Symbols name |
| FAB | Style | Primary, Secondary, Outlined |
| FAB | State | Enabled, Hovered, Focused, Pressed |

## Decision rules — choosing the button style

1. **High emphasis** — the most important action on the screen → `Style=Filled`.
2. **Medium emphasis** — important actions that shouldn’t distract from the main task → `Style=Tonal` (secondary colour mapping).
3. Use `Style=Elevated` (tonal with a shadow) only when the button needs separation from a visually prominent background, e.g. an image or scrim.
4. **Medium emphasis, alternative/secondary action** → `Style=Outlined`. Outlined pairs well with a Filled button.
5. **Lowest priority, optional actions** → `Style=Text`. In cards, Text buttons keep the emphasis on the card content.
6. **MUST** give the more important action the higher-emphasis style when buttons sit together: Filled + Text, Filled + Outlined, or Outlined + Text.
7. **SHOULD NOT** use more than one high-emphasis (Filled) action in the same area. **MUST NOT** emphasise a Filled button and a FAB together.
8. Outlined and Text buttons depend on colour to be recognisable; if they could be mistaken for plain text, use Filled or Tonal. Use caution placing Outlined buttons on images.

## Decision rules — icon buttons

1. **Filled** → high-emphasis key actions (e.g. download, delete).
2. **Tonal** → middle ground between Filled and Outlined.
3. **Outlined** → medium emphasis, e.g. previous/next arrows that show more content is available.
4. **Text (standard)** → low emphasis, or on a colourful surface.
5. In app bars and toolbars, use at most **one** Filled or Tonal icon button.
6. When all actions have the same emphasis, use icon buttons of the **same size**.
7. Icons: default icon buttons use filled icons. Toggle icon buttons use an outlined icon when unselected and the filled icon when selected.
8. **MUST NOT** use an icon button when the icon’s meaning is ambiguous — use a Button with a label.

## Decision rules — FAB

1. Use a FAB only for the **primary action of a screen**. (PDR: one FAB per screen.)
2. Use an extended FAB (icon + label) on long scrolling screens that need persistent access to an action, or when the icon alone is ambiguous.
3. **MUST NOT** use a FAB or extended FAB as one option in a set of actions — use Filled buttons instead.
4. Position the FAB so it never fully hides another element’s focus indicator.
5. PDR convention: on mobile, the page’s primary action becomes the FAB (see Page header).

## Behavior and interaction

- A button performs its action on click/tap; it doesn’t change the selection state of other items.
- On web, icon buttons **MUST** show a tooltip with their accessibility label on hover; a FAB’s tooltip shows its label when focused.

## States

| State | When | In Figma |
|---|---|---|
| Enabled | Default, interactive | `State=Enabled` |
| Hovered | Pointer over the button (web) | `State=Hovered` |
| Focused | Keyboard focus | `State=Focused` |
| Pressed | During click/tap | `State=Pressed` |
| Disabled | Action currently unavailable | `State=Disabled` (Button, Icon button) |
| Loading | PDR: action in progress | `State=Loading` (Button, Icon button) |

## Content guidelines

- Labels describe the action and use **sentence case** (capitalise the first word and proper nouns), e.g. “Neuer Vorgang”.
- **MUST NOT** truncate or wrap label text; keep it on one line.
- Keep the icon and label grouped and centered as the button width changes.
- Icon button and FAB accessibility labels describe the action, e.g. “Add to favorites”, “Compose a new message”.

## Usage guidelines

| Do | Don’t |
|---|---|
| Pair a Filled primary action with an Outlined or Text alternative | Put two Filled buttons side by side |
| Use Text buttons for low-priority actions in cards and dialogs | Use a FAB as one option in a set of actions |
| Use one Filled/Tonal icon button for the key action in an app bar | Use several Filled/Tonal icon buttons in one app bar |
| Keep all icon buttons the same size when they have equal emphasis | Use an icon whose meaning isn’t clear |

## Combining with other components

- **Page header (PDR):** secondary page-level actions sit on the right side of the primary action in the same size. Tablet: secondary actions go into a ⋮ icon button. Mobile: the primary action becomes a FAB.
- **Snackbar:** at most one Text button; never Filled or Elevated.
- **Toolbars / app bars:** icon buttons with an even hierarchy; one Filled icon button may add emphasis to a single action.

## Accessibility

- **MUST** keep a 48 × 48 px target for every button and icon button, even when the visible button is smaller.
- **MUST NOT** apply density to buttons by default.
- Keyboard: **Tab** moves focus to the button; **Space** or **Enter** activates it.
- Icon buttons and FABs **MUST** have an accessibility label describing the action.

## AI checklist

- [ ] Exactly one high-emphasis action per area (Filled or FAB, not both)
- [ ] Style matches importance: Filled > Tonal/Elevated > Outlined > Text
- [ ] Icon buttons only for unambiguous icons; same size when equal emphasis
- [ ] FAB only for the screen’s primary action
- [ ] Labels describe the action; icon-only buttons have an accessibility label and tooltip
- [ ] 48 × 48 px targets

## Not covered by M3 (PDR conventions)

- **Loading state:** documented in Figma but not on the M3 buttons pages.
- **FAB styles:** Primary, Secondary and Outlined are PDR variants. The Figma FAB has no size or extended-label variants.
- **Icon button and FAB Elevated styles:** PDR extensions. An elevated icon button isn’t defined in M3 or Angular Material.

---

# Part 2 — Angular implementation

### Button — `10007:3190`


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

#### `pdr-button` (loading wrapper)

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

### Icon button — `10007:3136`


Props: `Size` Small|Medium|Large · `Style` Filled|Outlined|Text|Tonal|Elevated · `State` …|Loading

| Figma | Angular |
|---|---|
| Style=Text | `<button matIconButton aria-label="…">` (default) |
| Style=Filled / Tonal / Outlined / Elevated | `matIconButton` + `class="pdr-icon-btn--filled|--tonal|--outlined|--elevated"` |
| Size=Small 32 / Medium 40 / Large 48 | `pdr-icon-btn--sm` / default / `pdr-icon-btn--lg` |

`aria-label` is mandatory. Icon color default = `on-surface-variant` (Figma `icon-standard/content`).

### FAB — `4157:32313`


Props: `Style` Primary|Secondary|Outlined · 56×56, `corner-large`, level3

| Figma | Angular |
|---|---|
| Style=Secondary | `<button matFab>` (M3 default = primary-container) |
| Style=Primary | `<button matFab class="pdr-fab--primary">` |
| Style=Outlined | `<button matFab class="pdr-fab--surface">` |
| Extended (label) | `<button matFab extended>` |

### Overrides (`styles/components/md3/_buttons.scss`)

> **Check with design:** Part 1 says Tonal uses the “secondary colour mapping” (M3 wording), but the Figma `Button color` variables set the Tonal container to **primary-container**, so the override below follows the Figma variables. Confirm which one is intended.


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
