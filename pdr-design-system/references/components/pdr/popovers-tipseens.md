# Popovers & Tipseens

Figma page: **Popovers & Tipseens** `3330:123` · status 🌕 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-123)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

> 🌕 Not final in Figma. Use Material defaults / minimal styling and flag deviations in the PR.

## Components
- **Onboarding tipseen** `8110:19234` — `Alignment` on bottom|on top; **Walkthrough tipseen** `4291:9171`
- **Onboarding modal** `10697:44819` — `Size` Mobile|Tablet and desktop; **Onboarding modal v1** `4528:21538`, **Welcome illustration** `4528:14510`
- **Module popover** `7742:11750`
- **Video frame** `10163:4143`, **Video player** `10320:6802`

## Mapping
| Figma | Wrapper | Built from |
|---|---|---|
| Onboarding / Walkthrough tipseen | `<pdr-tipseen [anchor] position="below|above" [step] [total]>` | `cdkConnectedOverlay` (inverse-surface or primary per Figma, `corner-medium`, level2, arrow), `matButton` "Weiter"/"Überspringen" |
| Onboarding modal (+Mobile) | `MatDialog` with `panelClass: ['pdr-dialog','pdr-onboarding']`, width `--pdr-dialog-width-l`; mobile full-screen | see `../md3/dialogs.md` |
| Module popover | `<pdr-module-popover>` | `cdkConnectedOverlay`, surface-container-lowest, `corner-large`, level3 |
| Video frame / player | `<pdr-video-player [src]>` | native `<video controls>` + captions track |

Tipseen: focus moves into the tipseen, Esc closes, completion persisted per user.
