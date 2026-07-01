---
name: figma-ui-export
description: Use when recreating UI screenshots or visual references as high-fidelity editable Figma files, preparing sliceable Figma exports, exporting an existing Figma frame to standalone HTML/CSS/assets, or producing a local .fig file for design handoff/import tools. Trigger phrases include screenshot to Figma, Figma slicing, figma-export-html, figma-export-file, Figma to HTML, export HTML from Figma, export .fig, 蓝湖/Lanhu/Blue Lake import, and Figma as the only source.
---

# Figma UI Export

## Core Principle

Choose the right output mode and layer granularity. UI chrome and interface text should stay editable. Complex authored visuals should stay atomic. Never turn a screenshot or full Figma frame into the final flattened output when the user needs editable design, HTML, or a `.fig` handoff file.

## Modes

| Mode | Source | Output | Key rule |
|---|---|---|---|
| `screenshot-to-figma` | Screenshot, prototype image, visual reference | Editable, sliceable Figma file | Recreate the UI in Figma; do not claim a screenshot can be mechanically converted. |
| `figma-export-html` | Existing Figma frame | Standalone `index.html`, `styles.css`, `assets/` | Treat the Figma frame as the source of truth; do not reuse project HTML/CSS/JS/assets unless explicitly allowed. |
| `figma-export-file` | Existing Figma file, page, or frame | Local `.fig` file | Export a real Figma local copy for import into design handoff tools; do not fake it by renaming another format. |

## Granularity Rules

| Element type | Treatment |
|---|---|
| Status bars, navigation, cards, forms, tabs, buttons, chips, tags, simple badges, simple backgrounds | Editable UI layers or DOM/CSS |
| Interface copy, labels, values, metadata, state text | Editable text layers or DOM text |
| Simple action/status/navigation symbols | Vector icons, preferably SVG |
| Composed hero/editorial/promo panels, rich media, realistic renders, photos, avatars, complex decorative art, chart snapshots | Atomic bitmap assets |
| Atomic visuals that contain visible text or objects | Keep atomic unless the user asks to edit internals |

## Screenshot To Figma

1. Inspect the reference.
   - Measure canvas size, safe areas, section bounds, repeated components, spacing, colors, typography, shadows, radii, asset scale, fixed/sticky elements, and overflow behavior.
   - List export candidates: icons, embedded media, illustrations, photos, backgrounds, badges, logos, and complex visual modules.

2. Recreate the Figma file.
   - Place the source image in a locked `reference/original-image-locked` frame.
   - Create the main frame at the source dimensions unless the user asks otherwise.
   - Recreate interface copy as editable text. Do not flatten UI text into images.
   - Use high-quality generated/redrawn bitmap assets only for complex visual modules.
   - Use Auto Layout for structurally related sections, lists, cards, toolbars, and repeated rows where practical.
   - Turn repeated UI structures into components when it improves editing or slicing.

3. Organize for export.
   - Use clear prefixes: `section/`, `component/`, `asset/`, `icon/`, `reference/`, `internal/`, `notes/`, `slices/export`.
   - Name atomic visuals clearly, for example `asset/hero-visual-atomic`, `asset/rich-panel-atomic`, `asset/media-object-atomic-01`.
   - Set bitmap exports to PNG 2x by default; set vector icons to SVG.

4. Verify.
   - Compare the recreated frame against the reference at whole-screen and key-section scales.
   - Fix major deviations in layout, spacing, font size/weight, color, radii, shadows, icon scale, asset scale, alignment, and visual density.
   - Confirm no final asset is a direct crop from the original screenshot.
   - Confirm editable UI remains editable and atomic visuals are intentionally atomic.

## Figma Export HTML

1. Lock the source frame.
   - Identify the exact file key, page, and frame node ID.
   - Export only the requested frame unless the user asks for multiple frames.
   - Ignore `reference/`, `notes/`, construction layers, helper canvases, and `slices/export` as visible page content.

2. Read Figma before writing code.
   - Use metadata, design context, and a frame screenshot to capture bounds, names, fills, effects, text, typography, colors, radii, hierarchy, and QA evidence.
   - Preserve intentional fallback or placeholder states from Figma. Do not repair them with local project files unless explicitly instructed.

3. Export local assets.
   - Export `asset/*-atomic` and complex visual modules as bitmap files.
   - Export simple symbols as SVG when possible.
   - Save every used asset under the new output folder's `assets/`.
   - Do not leave short-lived Figma URLs, unrelated remote URLs, or existing project asset paths in final HTML/CSS.

4. Generate standalone HTML/CSS.
   - Prefer `figma-html-export/<frame-slug>/` with `index.html`, `styles.css`, and `assets/`.
   - Map clear layer groups to semantic HTML such as `header`, `nav`, `main`, `section`, `article`, `button`, and `a`.
   - Preserve useful `data-node-id` and `data-name` attributes for traceability.
   - Use Figma absolute coordinates for the first fidelity pass when visual matching matters.
   - Match dimensions, spacing, typography, colors, gradients, opacity, radii, shadows, clipping, z-order, and image fit.
   - Add a viewport scale wrapper for fixed prototype canvases.
   - Keep interactions prototype-level only; do not add business logic or navigation not present in Figma.

5. Verify.
   - Render locally by static server or direct file open when sufficient.
   - Capture a browser screenshot at the Figma frame size and compare it with the Figma screenshot.
   - Check key module boxes, overlap, clipping, scaling, and text fit.
   - Confirm all image and SVG requests succeed.
   - Search final HTML/CSS for old prototype folders, remote Figma asset URLs, unrelated local asset paths, and unrequested external dependencies.
   - Report the output folder, verification result, and any preserved Figma fallback states.

## Figma Export File

Use this mode when the user needs a `.fig` file for import into 蓝湖/Lanhu/Blue Lake or another design handoff tool.

1. Define the export scope.
   - Confirm whether the output should contain the whole file, selected pages, or selected frames.
   - For a single-frame handoff, prefer duplicating the target frame into a clean temporary Figma file or page before export.

2. Prepare the Figma content.
   - Preserve editable layers, text, components, variables/styles, export settings, and atomic assets needed by the handoff target.
   - Remove or hide non-delivery material such as locked references, QA screenshots, notes, construction layers, helper canvases, and unrelated pages.
   - Keep clear layer names and section/component/asset/icon prefixes when they help downstream inspection.

3. Export a real `.fig`.
   - Use Figma's native local-copy export path, such as desktop/browser `Save local copy`, when programmatic tooling cannot produce `.fig`.
   - Save the file with a clear name, for example `<screen-or-project>-handoff.fig`.
   - Never rename PNG, SVG, ZIP, HTML, or screenshots to `.fig`.

4. Verify handoff readiness.
   - Confirm the `.fig` file exists and has nonzero size.
   - Reopen or re-import it when possible to confirm the target frame/page, editable text, and major assets survived.
   - Note any limitations caused by unavailable native export access, missing fonts, unpublished library components, or third-party importer constraints.

## Quality Rules

- Preserve the source's functional meaning, hierarchy, interaction intent, and visual density.
- Prefer fewer high-quality atomic assets over many weak approximate pieces.
- Keep generated asset resolution comfortably above displayed size.
- Use only source-provided, generated, or explicitly allowed resources.
- For `.fig` handoff, preserve editability and remove non-delivery layers instead of flattening the design.
- Keep the skill generic: do not encode domain-specific products, industries, page names, or one-off project examples.

## Do Not

- Use the whole screenshot or full Figma frame as the final deliverable.
- Crop icons, rich visuals, photos, or UI fragments from a screenshot for final assets.
- Split composed visuals into fake editable pieces.
- Substitute rich visuals with simplistic placeholders.
- Merge unrelated exports when they should be sliced separately.
- Deliver a fake `.fig` file made by renaming another file type.
- Add non-source features, repaired content, replacement assets, or implementation strategy not requested by the user.
