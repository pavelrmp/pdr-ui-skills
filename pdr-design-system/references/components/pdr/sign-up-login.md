# Sign up & Login

Figma page: **Sign up & Login 🟢** `3330:126` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-126) · Figma Spec: [`11038:3958`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11038-3958)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma components:** `Sign-up and login panel`; reference frame “Anmelden” · **Angular:** custom PDR component (selector to confirm) · **Sources:** components on this page; PDR Brand loader, Form fields and Skeleton/Error states specs

> **No M3 component.** Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

The sign-up and login panel is where people sign in to PDR.cloud, confirm their identity (authentication / MFA) and see what to do when the connection fails.

## Figma component and properties

| Property | Values |
|---|---|
| Screen | Login, Authentication, Network error |

## Decision rules

1. Login → `Screen=Login` (e-mail and password, language switch “DE”); 6-digit code after login → `Screen=Authentication`; sign-in from a network that isn’t allowed (e.g. IP restriction) → `Screen=Network error` (“Unzulässiges Netzwerk”).
2. After the credentials or code are submitted, show the **Brand loader (Wordmark)** full-screen while the session loads; the same on logout. *(Brand loader rules)*
3. Form fields follow the **Form fields** rules: labels on every field, errors inline replacing supporting text.
4. (PDR proposal — confirm) The primary action (“Anmelden”) is the only Filled button on the panel.
5. `Screen=Network error` is about a **disallowed** network, not a missing connection. When the device is offline, use `Error state/No connection` instead. *(PDR proposal — confirm)*

## AI checklist

- [ ] Correct Screen for the step
- [ ] Brand loader after submitting, not a spinner
- [ ] Labelled fields, inline errors
- [ ] One Filled primary action

## Open questions for the team

- **Typo:** “Unzulassiges Netzwerk” → “Unzulässiges Netzwerk”.
- **Language:** the Authentication screen is in English (“Enter a 6-digit code…”), the other screens in German. Translate consistently.
- **Sign up:** the component is named “Sign-up and login”, but there’s no sign-up screen. Is sign-up handled elsewhere?
- **Password reset:** is there a “Passwort vergessen” flow to document?
- **Deprecated layers:** the panel still contains 4 `Deprecated/…` layers.

---

# Part 2 — Angular implementation

### API

```html
<pdr-auth-panel [screen]="'login'|'authentication'|'network-error'" />
```
| Figma Screen | Content |
|---|---|
| Login | `mat-card` (surface-container-lowest, `corner-extra-large`) + `pdr-brand-loader variant="wordmark"` + email/password `mat-form-field appearance="outline"` (`autocomplete="username"/"current-password"`, show/hide password `matIconButton matSuffix`) + `matButton="filled"` full width |
| Authentication (MFA) | `<pdr-code-input [length]="6">` (see `../md3/form-fields.md`) + resend text `matButton` |
| Network error | `<pdr-error-state type="no-connection">` + retry `matButton` |

Width `--pdr-dialog-width-m` (420), centered; errors via `<mat-error>` and a `pdr-alert type="error"` for server errors.
