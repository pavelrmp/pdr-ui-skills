# Motion

Figma: **⚛️ Design Tokens** page `3313:3` · [Animation](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=6463-29546)
Machine-readable source: `../../tokens.json`. Theme setup: `../theming-rules.md`.

The Figma **Animation** frame has no motion tokens yet. Until it does:

1. Use Angular Material’s built-in component animations — don’t restyle them.
2. Custom transitions: 150–250 ms, `cubic-bezier(0.2, 0, 0, 1)` (M3 standard easing) for enter/exit; 100 ms for hover/state changes.
3. Brand loader timings are defined in `../components/pdr/brand-loader.md`.
4. Always respect `prefers-reduced-motion` (global rule in `../foundations/accessibility.md`).

When motion tokens are added in Figma, document them here and in `tokens.json`.
