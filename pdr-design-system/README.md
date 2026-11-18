# PDR.cloud Design System — Claude skill

Claude skill + design tokens that map the [PDR.cloud Figma Design System](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System) to **Angular Material M3 (≥ v20)**.

| Path | Contents |
|---|---|
| `SKILL.md` | Router, guardrails, Figma → Angular index |
| `tokens.json` | DTCG / Style Dictionary v4 tokens (light + dark, M3 roles, PDR roles, typescale, shape, elevation, spacing) |
| `references/theming-rules.md` | `mat.theme()` setup, `--mat-sys-*` / `--pdr-*` properties, override rules |
| `references/components/md3/` | One file per Figma page under "↓ ANGULAR MD3 COMPONENTS" |
| `references/components/pdr/` | One file per Figma page under "↓ PDR COMPONENTS" |
| `references/foundations/` | Accessibility, grids & breakpoints, icons |
| `references/examples/` | Page examples from the Figma "Examples" page |

## Install

**Claude Code**
- Project (recommended, shared with the team via git): put this folder at `.claude/skills/pdr-design-system/` in the root of the Angular repo.
- Personal (all your projects): `~/.claude/skills/pdr-design-system/`.
- The folder name must stay `pdr-design-system` (same as `name` in `SKILL.md`). Claude loads it automatically for UI work, or run `/pdr-design-system`.
- Connect the Figma MCP server so Claude can open Figma frames and icons by node ID.

**Claude (claude.ai / desktop)**
- Upload `pdr-design-system.zip` (this folder at the top level of the zip) under Settings → Capabilities → Skills.

Tokens were extracted via Figma MCP on 2026-11-18. Re-extract when Figma variables change.
