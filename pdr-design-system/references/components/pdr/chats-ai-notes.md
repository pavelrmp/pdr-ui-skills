# Chats, AI & Notes

Figma page: **Chats, AI & Notes 🌕** `3330:112` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=3330-112) · Figma Spec: [`11036:8230`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=11036-8230)
Layer: **PDR** — no Material equivalent; compose Material primitives + tokens. Tokens: `../../tokens/`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🌕 In progress · **Figma components:** `Chat`, `Chat menu`, `Message input`, `AI response`, `User response`, `Notes workshop`, `Notes new`, `Notes new pinned`, `Workshop new note`, `Workshop new note confirm`, `Workshop info`, `Workshop info visibility`, `New message content`, `Changes` · **Angular:** custom PDR components (selectors to confirm) · **Sources:** component properties and descriptions on this page

> **No M3 component.** Chats, AI conversations and notes are PDR patterns. Rules marked **(PDR proposal — confirm)** need the team’s confirmation.

Rule strength: **MUST** = mandatory · **SHOULD** = recommended · **MAY** = optional.

## Purpose

| Area | Components | Use |
|---|---|---|
| **Chat** (people) | `Chat menu` (conversation list), `Chat` (thread), `Message input` | Conversations between users, e.g. about an order |
| **AI assistant** | `AI response`, `User response`, `Message input` | Conversation with PDR AI (e.g. photo-based damage assessment) |
| **Notes** | `Notes workshop`, `Notes new`, `Notes new pinned`, `Workshop new note` (+ confirm), `Workshop info` (+ visibility) | Internal notes on an order or vehicle for the workshop team |

## Figma components and properties

| Component | Properties |
|---|---|
| Chat | Type: Message, My reply, Important, Empty · State: Enabled, Hovered · Show badge · Instance (swap) |
| Chat menu | State: Enabled, Hovered, Selected — one conversation row (avatar, name, time, last message) |
| AI response | Example: Answer 1, AI Answer 4, AI Answer 5 (reference answers) |
| User response | Type: My Text, My Photo |
| Notes workshop | Content: Filled, Empty |
| Message input · Notes new · others | No properties |

## Decision rules

1. Conversations between people → **Chat** components; conversations with the AI assistant → **AI response / User response**. **MUST NOT** mix them in one thread. *(PDR proposal — confirm)*
2. AI messages are always labelled as AI (“PDR AI”) and use the AI avatar (Avatars › Category=AI). *(PDR proposal — confirm)*
3. (PDR proposal — confirm) `Chat · Type=Important` only for messages that need attention; `Type=Empty` when a conversation has no messages yet.
4. Exactly one conversation in `Chat menu` is `State=Selected` — the open thread.
5. Notes are internal (workshop team), chats are communication. Use `Workshop info visibility` to show who can see a note. *(PDR proposal — confirm)*
6. Empty states: `Notes workshop · Content=Empty`, `Chat · Type=Empty`.

## Content guidelines

- Each message shows author, time (e.g. “22.03.24 12:32”) and text.
- AI answers stay short and actionable; long results go into the order data, not the chat. *(PDR proposal — confirm)*

## AI checklist

- [ ] Chat for people, AI response for the assistant
- [ ] AI clearly labelled with the AI avatar
- [ ] One selected conversation
- [ ] Empty states used when there is no content

## Open questions for the team

- **Deprecated layers:** `Chat`, `Message input`, `AI response`, all Notes components and `Changes` still contain `Deprecated/Button`. Swap to the current Button.
- **Unused components:** `User response`, `Workshop new note` (+ confirm), `Workshop info` (+ visibility), `Notes new pinned`, `New message content` and `Changes` have no uses in this file. Which are current?
- **Examples vs components:** `AI response` variants are example answers (`Answer 1`, `AI Answer 4/5`). Should it become one component with a content slot?
- **Message input:** no properties for attachments, voice or AI actions. What does it support in code?
- **Notes visibility:** what are the visibility levels (team, branch, customer)?

---

# Part 2 — Angular implementation

### Mapping

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

### A11y

Message list `role="log"` `aria-live="polite"`; Enter sends, Shift+Enter newline.
