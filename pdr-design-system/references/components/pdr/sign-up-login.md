# Sign up & Login

Figma page: **Sign up & Login** `3330:126` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-126)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

## Components
- **Sign-up and login panel** `10672:39610` — `Screen` Login|Authentication|Network error

## API
```html
<pdr-auth-panel [screen]="'login'|'authentication'|'network-error'" />
```
| Figma Screen | Content |
|---|---|
| Login | `mat-card` (surface-container-lowest, `corner-extra-large`) + `pdr-brand-loader variant="wordmark"` + email/password `mat-form-field appearance="outline"` (`autocomplete="username"/"current-password"`, show/hide password `matIconButton matSuffix`) + `matButton="filled"` full width |
| Authentication (MFA) | `<pdr-code-input [length]="6">` (see `../md3/text-fields.md`) + resend text `matButton` |
| Network error | `<pdr-error-state type="no-connection">` + retry `matButton` |

Width `--pdr-dialog-width-m` (420), centered; errors via `<mat-error>` and a `pdr-alert type="error"` for server errors.
