# Icons

Figma page: **24px Icons 🟢** `3345:93168` · custom set **PDR Icons** `6106:3674`

**Source of truth for PDR icons: [PDR Icons in Figma](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=6106-3674)**. The SVGs are not shipped with this skill — always take them from Figma.

## Two icon sources

| Need | Use |
|---|---|
| Generic UI icon (edit, delete, search, chevrons…) | **Material Symbols Outlined** — `<mat-icon fontSet="material-symbols-outlined">edit</mat-icon>` |
| Filled variant of a Material Symbol | add `class="pdr-icon--filled"` (`font-variation-settings: 'FILL' 1`) |
| Domain icon (paint, bodywork, parts, car views, order states…) | **PDR icons** — `<mat-icon svgIcon="pdr:engine">` |

Never mix in other icon libraries, never inline raw `<svg>` in templates, never use PNG icons. Size is always 24 px (`--mat-icon-size` default); 18 px only inside buttons/chips where Material does it automatically.

## PDR icon set (69 icons, 24 × 24) — [open in Figma](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=6106-3674)

In Figma the icons use fill `#344254` (cool grey/40). When exporting, replace it with `currentColor` so icons inherit text color (`--mat-sys-on-surface-variant` by default in icon buttons). Exception: `ai` keeps its brand color. `api_connect` is a status dot in Figma.

| Category | Icons |
|---|---|
| Lackierung (paint & workshop) | `paint`, `dents`, `electric`, `final_assembly`, `glass`, `detailing`, `final_control`, `paint_2`, `tools_power_drill`, `paint_preparation`, `paint_preparation_2`, `paint_preparation_2_filled`, `fuel` |
| Karosserie (bodywork) | `bodywork_1`, `bodywork_2`, `bodywork_3` |
| Services | `car_gear`, `auto_towing`, `swap_driving_apps`, `paint_3`, `paint_4` |
| Autoteile (parts) | `car_door`, `tire`, `tire_flat`, `steering_wheel`, `brakes_2`, `suspension`, `key`, `key2`, `key3`, `mechanic`, `brakes_sign`, `engine`, `engine_filled`, `brakes`, `brakes_filled`, `oil`, `oil_filled`, `spare_part`, `spare_part_filled` |
| Car views | `car_front`, `car_back`, `car_side`, `car_top`, `car_interior`, `car_details`, `eraser` |
| AI tools | `smart_docs`, `daily_meeting`, `ai`, `comparison`, `comparison_filled` |
| Aufträge (order states) | `in_process`, `canceled`, `uninvoiced`, `accepted` |
| Delivery | `destruction`, `parts_delivery`, `parts_delivery_broken`, `parts_delivery_broken_filled` |
| API | `api_connect` |
| Brand | `pdr_logo_24px` |
| Social media | `behance`, `dribbble`, `facebook3`, `instagram`, `linkedin`, `twitter`, `youtube` |

Outlined/Filled pairs: `engine` / `engine_filled`, `brakes` / `brakes_filled`, `oil` / `oil_filled`, `spare_part` / `spare_part_filled`, `paint_preparation_2` / `paint_preparation_2_filled`, `comparison` / `comparison_filled`, `parts_delivery_broken` / `parts_delivery_broken_filled`. Use Filled for selected/active states only.

Social icons (`behance`, `dribbble`, `facebook3`, `instagram`, `linkedin`, `twitter`, `youtube`) are for footers/marketing only.

## Setup (once)

1. Get the SVGs from [PDR Icons in Figma](https://www.figma.com/design/3N1iHNzVKurYAwq0LWsVpQ/PDR.cloud-Design-System?node-id=6106-3674) into `src/assets/icons/pdr/` in the app (file name = icon name, e.g. `engine.svg`):
   - **Manually:** select the icon component in Figma → right panel **Export** → SVG → Export. Then replace `fill="#344254"` with `fill="currentColor"`.
   - **With Claude + Figma MCP:** ask Claude to export the icon by its node ID (table below) with `use_figma` → `exportAsync({ format: 'SVG_STRING' })`, replace `#344254` with `currentColor`, and save it to `src/assets/icons/pdr/<name>.svg`.
   - Only add the icons the app actually uses.
   - File names use underscores: Figma `car/front` → `car_front.svg`, `comparison 1` → `comparison.svg`, Filled variants → `<name>_filled.svg`.
2. Register the namespace:

```ts
// app.config.ts
import { provideHttpClient } from '@angular/common/http';
import { inject, provideAppInitializer } from '@angular/core';
import { MatIconRegistry } from '@angular/material/icon';
import { DomSanitizer } from '@angular/platform-browser';
import { PDR_ICONS } from './pdr-icons';

export const appConfig = {
  providers: [
    provideHttpClient(),
    provideAppInitializer(() => {
      const registry = inject(MatIconRegistry);
      const sanitizer = inject(DomSanitizer);
      registry.setDefaultFontSetClass('material-symbols-outlined');
      for (const name of PDR_ICONS) {
        registry.addSvgIconInNamespace('pdr', name, sanitizer.bypassSecurityTrustResourceUrl(`assets/icons/pdr/${name}.svg`));
      }
    }),
  ],
};
```
```ts
// pdr-icons.ts — list of icons present in src/assets/icons/pdr (names = Figma layer names)
export const PDR_ICONS = ["accepted", "ai", "api_connect", "auto_towing", "behance", "bodywork_1", "bodywork_2", "bodywork_3", "brakes", "brakes_2", "brakes_filled", "brakes_sign", "canceled", "car_back", "car_details", "car_door", "car_front", "car_gear", "car_interior", "car_side", "car_top", "comparison", "comparison_filled", "daily_meeting", "dents", "destruction", "detailing", "dribbble", "electric", "engine", "engine_filled", "eraser", "facebook3", "final_assembly", "final_control", "fuel", "glass", "in_process", "instagram", "key", "key2", "key3", "linkedin", "mechanic", "oil", "oil_filled", "paint", "paint_2", "paint_3", "paint_4", "paint_preparation", "paint_preparation_2", "paint_preparation_2_filled", "parts_delivery", "parts_delivery_broken", "parts_delivery_broken_filled", "pdr_logo_24px", "smart_docs", "spare_part", "spare_part_filled", "steering_wheel", "suspension", "swap_driving_apps", "tire", "tire_flat", "tools_power_drill", "twitter", "uninvoiced", "youtube"] as const;
export type PdrIcon = typeof PDR_ICONS[number];
```

## Usage
```html
<mat-icon svgIcon="pdr:engine" aria-hidden="true" />
<button matIconButton aria-label="Lackierung"><mat-icon svgIcon="pdr:paint" /></button>
<pdr-status-tag status="info" display="icon-text"><mat-icon svgIcon="pdr:in_process" />In Bearbeitung</pdr-status-tag>
```
- Decorative icon next to text → `aria-hidden="true"`; icon-only control → `aria-label` on the button.
- Color via the parent's `color`, never via `fill` overrides.

## Icon → Figma node

When an icon changes or is added in Figma, re-export it the same way and add its name to `PDR_ICONS`. Variant pairs (`_filled`) are the `Property 1=Filled` variants of the same component set. Node IDs:

| Icon | Node | Icon | Node | Icon | Node |
|---|---|---|---|---|---|
| `paint` | `4856:21486` | `dents` | `4856:21801` | `electric` | `4856:21806` |
| `final_assembly` | `4856:21504` | `glass` | `6119:10419` | `detailing` | `4856:21500` |
| `final_control` | `4856:21495` | `paint_2` | `9931:2252` | `tools_power_drill` | `6112:4108` |
| `paint_preparation` | `9931:2316` | `paint_preparation_2` | `4856:21468` | `paint_preparation_2_filled` | `8548:5627` |
| `fuel` | `9933:4104` | `bodywork_1` | `4856:21925` | `bodywork_2` | `6118:7497` |
| `bodywork_3` | `6118:7506` | `car_gear` | `6112:10932` | `auto_towing` | `6120:12808` |
| `swap_driving_apps` | `6120:12809` | `paint_3` | `9933:4132` | `paint_4` | `9933:4366` |
| `car_door` | `6108:3349` | `tire` | `6110:3397` | `tire_flat` | `6116:7436` |
| `steering_wheel` | `6116:7401` | `brakes_2` | `6116:7325` | `suspension` | `6116:6469` |
| `key` | `6116:7359` | `key2` | `10103:4698` | `key3` | `10103:4753` |
| `mechanic` | `4856:21795` | `brakes_sign` | `6115:6415` | `engine` | `6109:3387` |
| `engine_filled` | `7898:45834` | `brakes` | `6108:3377` | `brakes_filled` | `7898:45837` |
| `oil` | `6116:7336` | `oil_filled` | `7898:45861` | `spare_part` | `6116:7419` |
| `spare_part_filled` | `8548:5624` | `car_front` | `3952:4463` | `car_back` | `3952:4465` |
| `car_side` | `3952:4470` | `car_top` | `3952:4472` | `car_interior` | `3952:4474` |
| `car_details` | `3952:4476` | `eraser` | `3952:4478` | `pdr_logo_24px` | `5696:35264` |
| `behance` | `7531:39538` | `dribbble` | `7531:39539` | `facebook3` | `7531:39540` |
| `instagram` | `7531:39541` | `linkedin` | `7531:39542` | `twitter` | `7531:39543` |
| `youtube` | `7531:39544` | `smart_docs` | `8522:431` | `daily_meeting` | `10120:1553` |
| `ai` | `9903:40418` | `comparison` | `10540:2102` | `comparison_filled` | `10561:7168` |
| `in_process` | `8616:16059` | `canceled` | `8616:16078` | `uninvoiced` | `8616:16109` |
| `accepted` | `8616:16108` | `api_connect` | `9785:11566` | `destruction` | `9856:19936` |
| `parts_delivery` | `9856:19940` | `parts_delivery_broken` | `9856:19946` | `parts_delivery_broken_filled` | `9856:19973` |
