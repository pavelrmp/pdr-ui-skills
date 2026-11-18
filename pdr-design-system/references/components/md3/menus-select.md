# Menus & Select

Figma page: **Menus & Select** `3330:97` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-97)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Dropdown** `3614:2484` — `Style` Standard|Filled|Outlined · `State` Enabled|Hovered|Focused|Error|Disabled · 56px
- **Menu list item 48** `3658:1567` — `State` Enabled|Hovered|Selected|Divider · `Type` Default|Checkboxes|1st · body-large
- **Menu list item 56** `3501:101` — `State` · `Level` 1st|2nd
- **Dropdown menu** `3658:2400`, **Dropdown menu clients** `3789:1431`, **Menu items divider** `4088:10910`
- `Example/Dropdown menu` `10723:16406` — reference only

## Select (form control)
| Figma Dropdown Style | Angular |
|---|---|
| Outlined | `<mat-form-field appearance="outline"><mat-select>` |
| Filled | `appearance="fill"` |
| Standard | `appearance="fill"` + `pdr-field--transparent` (see `text-fields.md`) |
| State=Error | validator + `<mat-error>` |

```html
<mat-form-field appearance="outline">
  <mat-label>Status</mat-label>
  <mat-select formControlName="status">
    @for (s of statuses; track s.id) { <mat-option [value]="s.id">{{ s.label }}</mat-option> }
  </mat-select>
</mat-form-field>
```

## Menu (actions)
| Figma | Angular |
|---|---|
| Dropdown menu | `[matMenuTriggerFor]="menu"` + `<mat-menu #menu>` |
| Menu list item 48 Default | `<button mat-menu-item>` (+ `<mat-icon>` leading) |
| Type=Checkboxes | `<button mat-menu-item role="menuitemcheckbox" [attr.aria-checked]>` with `<mat-pseudo-checkbox [state]>`; keep menu open via `(click)="$event.stopPropagation()"` |
| State=Selected | `class="pdr-menu-item--selected"` + `aria-current="true"` |
| Divider / Menu items divider | `<mat-divider>` |
| Menu list item 56 Level 2nd | nested `[matMenuTriggerFor]` on a `mat-menu-item` |
| Dropdown menu clients | menu with `<pdr-avatar size="s">` leading |

## Overrides (`styles/components/md3/_menus-select.scss`)
```scss
.pdr-menu-item--selected { background: var(--mat-sys-secondary-container); color: var(--mat-sys-on-secondary-container); }
.pdr-menu--wide { min-width: 280px; } // via panelClass / class on mat-menu
```
