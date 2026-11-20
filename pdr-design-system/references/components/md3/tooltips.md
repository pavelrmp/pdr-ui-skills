# Tooltips

Figma page: **Tooltips 🟢** `10745:46756` · [open page](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10745-46756) · Figma Spec: [`10987:33770`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10987-33770) · [`10987:33841`](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=10987-33841)
Layer: **MD3** — implement with Angular Material. Tokens: `../../tokens/`, theming: `../../theming-rules.md`.

> **How to read this file.** Part 1 is the **Figma Spec** — the design rules (source of truth, copied from Figma). Part 2 is the **Angular implementation** for this codebase. If Part 2 contradicts Part 1, follow Part 1 and flag the difference.

# Part 1 — Figma Spec

**Status:** 🟢 Ready · **Figma specs:** “Plain Tooltip”, “Rich tooltip” · **Angular:** `matTooltip` (plain); rich tooltip as a PDR overlay

## Plain tooltip

A tooltip explains a control or icon and adds context. It appears only on hover and contains text only.

### When to use

Used on elements that cannot fit the full name or require a brief explanation. For example: action bars, icons without text, shortened overly long names in a table.
Plain tooltips briefly describe a UI element. They're best used for labelling UI elements with no text, like icon-only buttons and fields.

### How it works

The tooltip appears when hovering over an element with a 400-millisecond delay. This prevents flickering of hints when moving the cursor across the page.

The tooltip disappears immediately as soon as the cursor leaves the element. It also disappears if the page is scrolled after the hint appears.

The tooltip should fully replace standard browser tooltips in the interface, instead of system tooltips from alt and title tags.

### Text

The tooltip text should be as short as possible, ideally no more than 70 characters.

If the tooltip needs to display the name of an entity and it is long, don’t worry about the 70-character limit and display it.

The tooltip cannot contain instructions.

Do not duplicate the object’s name in the tooltip.

### Placement

By default, plain tooltips are positioned directly above the parent element.

- If there's a visual boundary, like a button, the distance is 4dp
- If there's no visual boundary, like with text baselines, the distance is 8dp

If the element is in an app bar, the plain tooltip appears below the element at the same distance.

The tooltip appears above the element it relates to. If there is no space above, it opens below. You can specify priority—above or below, and even left or right.

## Rich tooltip

A rich tooltip explains a control’s state, provides contextual help, or offers guidance and onboarding.

A rich tooltip opens on click, focus, hover, or a contextual trigger. It keeps the interface concise by placing supplementary information in a separate layer.

### When to use

Rich tooltips provide additional context about a UI element. They can optionally contain a subhead, buttons, and hyperlinks. Rich tooltips are best used for longer text like definitions or explanations.

Use a rich tooltip to clarify the state of an interface or control, provide help, or explain a term.

If an explanation requires more than 500 characters, consider writing an article and linking to it from the rich tooltip.

### Behavior

To show help or supplementary information, make the entire control—for example, a link or icon—clickable.

The interface icon library includes several options for help and supplementary information: a standard contextual help icon, a more subtle version of the help icon, and an information icon for supplementary details rather than help.

Do not use the user guide icon to open a rich tooltip with contextual help. Reserve it for links to the user guide.

### Subheads

Keep subheads brief, ideally to one line. They should summarize or describe the message of the rich tooltip.

Subheads are important to include when the rich tooltip appears automatically, like when the page loads.

### Text buttons (optional)

Rich tooltips can have up to two text buttons. These should be brief and relevant to the message in the supporting text.

Keep buttons short so they can be side by side. Avoid stacking them when possible.

### Size and placement

Keep rich tooltips compact and within the screen boundaries. They should not cover most of the screen. The recommended width of the rectangular body is 250 px; the maximum is 500 px.

Open the rich tooltip to the right of its trigger by default. If space is limited, try other positions in this order: right, above, left, below—moving counterclockwise.

Disable any placement that would obscure important information or other controls, and open the rich tooltip in another direction.

Align the rich tooltip’s pointer with the first character of its first line of text. This aligns the page text with the text inside the rich tooltip.

Keep a 2 px gap between the rich tooltip’s pointer and the object’s bounds. If the object’s bounds differ from its visible bounds by more than 16 px, use a 4 px gap from the visible bounds instead. See the Spacing and alignment guide for details.

Keep the rich tooltip’s opening direction unchanged while the page scrolls. For example, a rich tooltip that opens above its trigger must not flip to another side when scrolling brings it near the browser window’s edge.

---

# Part 2 — Angular implementation

### Mapping

| Figma | Angular |
|---|---|
| Plain tooltip `3736:1469` | `matTooltip="…"` (`matTooltipPosition` as designed). Defaults match. |
| Rich tooltip `10098:9303` | `<pdr-rich-tooltip>` via `cdkConnectedOverlay`: surface-container, `corner-medium`, level2, title-small heading + body-medium + optional text `matButton` actions |

Tooltips never hold the only copy of essential information; icon-only triggers still need `aria-label`.


```html
<button matIconButton matTooltip="Bearbeiten" aria-label="Bearbeiten"><mat-icon fontSet="material-symbols-outlined">edit</mat-icon></button>
```
Onboarding hints → `../pdr/popovers-tipseens.md`.

### Overrides (`styles/components/md3/_tooltips.scss`)

```scss
.pdr-rich-tooltip {
  background: var(--mat-sys-surface-container);
  border-radius: var(--mat-sys-corner-medium);
  box-shadow: var(--mat-sys-level2);
  max-width: 312px;
  padding: var(--pdr-space-12) var(--pdr-space-16) var(--pdr-space-8);
}
```
Plain tooltip = M3 default.
