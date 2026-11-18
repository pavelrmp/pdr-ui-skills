# Tabs, Steppers

Figma page: **Tabs, Steppers** `3330:127` · status 🟢 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-127)
Layer: **MD3** — must be implemented with Angular Material. Rules and tokens: `../../theming-rules.md`.

## Components
- **Tab** `3386:29` — `Selected` True|False · `State` Enabled|Hovered · 48px, title-small
- **Tabs** `3386:23`
- **Stepper** `3537:58` — `Type` Default|compact|Application

## Tabs
| Figma | Angular |
|---|---|
| Tabs (content switching) | `<mat-tab-group [(selectedIndex)] mat-stretch-tabs="false" mat-align-tabs="start">` + `<mat-tab label>` |
| Tabs (routing) | `<nav mat-tab-nav-bar [tabPanel]="panel">` + `<a mat-tab-link routerLinkActive [active]>` + `<mat-tab-nav-panel #panel>` |
| Selected=True | `selectedIndex` / `active` |
| Tab with badge/icon | `<ng-template mat-tab-label>` |

Lazy tab content: `<ng-template matTabContent>`.

## Stepper
| Figma Type | Angular |
|---|---|
| Default | `<mat-stepper [linear]="true" #s>` + `<mat-step [stepControl] label>`; buttons `matStepperNext` / `matStepperPrevious` |
| compact | `<pdr-wizard-steps variant="compact">` (see `../pdr/workflows.md`) |
| Application | `<pdr-wizard-steps variant="application">` |
| Vertical on mobile | `orientation="vertical"` via `BreakpointObserver` |

## Overrides

None — Figma matches M3 defaults. Do not add any.
