# Chats, AI & Notes

Figma page: **Chats, AI & Notes** `3330:112` · status 🌕 · [open](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-112)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Selectors are the agreed convention; check `libs/ui` before creating new ones.

> 🌕 Not final in Figma. Use Material defaults / minimal styling and flag deviations in the PR.

## Components
- **Chat** `6169:31816` — `Type` Message|My reply|Important|Empty · `State` Enabled|Hovered
- **Chat menu** `6714:13605` — `State` Enabled|Hovered|Selected
- **AI response** `10711:4732`, **User response** `10711:4733` — `Type` My Text|My Photo
- **Message input** `3723:1268`, **New message content** `6447:3793`
- **Notes workshop** `6169:31862` — `Content` Filled|Empty; **Notes new / pinned** `6699:28435`, `6699:28441`; **Workshop new note (+confirm)** `10209:6408`, `10212:6982`; **Workshop info (+visibility)** `7114:75353`, `10212:7310`

## Mapping
| Figma | Wrapper | Built from |
|---|---|---|
| Chat Type=Message / My reply | `<pdr-chat-message [own]>` | bubble: surface-container-high (other) / primary-container (own), `corner-large` |
| Type=Important | `[important]="true"` → `--pdr-sys-warning-container` |
| Type=Empty | `<pdr-empty-state type="notes">` |
| Chat menu | `<pdr-chat-list-item>` | `mat-list-item` + `[activated]` |
| AI response / User response | `<pdr-ai-message>` / `<pdr-chat-message own>` | AI uses `pdr-avatar category="bot"`; markdown rendered safely (sanitized) |
| Message input | `<pdr-message-input (send)>` | `mat-form-field appearance="outline"` + `cdkTextareaAutosize` + send `matIconButton` (filled) + attach `matIconButton` |
| Notes workshop / Notes new / pinned | `<pdr-note [pinned]>` | `mat-card appearance="filled"`, pin `matIconButton` |
| Workshop new note (+confirm) | `<pdr-note-composer>` | `matInput` + `matButton="filled"` |
| Workshop info visibility | `mat-select` / `mat-button-toggle-group` | — |

## A11y
Message list `role="log"` `aria-live="polite"`; Enter sends, Shift+Enter newline.
