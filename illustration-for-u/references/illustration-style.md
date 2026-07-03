# Illustration for U Style Reference

## Core Style

- Illustration for U creates quiet inline visual essays for articles, documents, PRDs, and campaign materials.
- The environment is a clean annotated-node/storyboard scene: one or more small cutout-like objects and story nodes on a calm, consistent background. Use thin hand-drawn black lines or arrows only when the article moment needs sequence, movement, comparison, causality, or a journey.
- The default background color is `#F4F4F2`, but a user-specified background color always takes priority. Keep the resolved background color consistent across the whole package unless the user asks for variation.
- The protagonist is a reusable article-illustration character. The bundled preset is 粉色海星 in `../assets/character-reference.png`, but users can replace it with their own character reference image or a text-defined character.
- The style split is intentional: objects, paper scraps, tape tabs, lighting, and shadows can be cutout-like or soft 3D; the protagonist keeps the rendering mode, line style, colors, and identity from the selected character reference.
- Use the number of visual nodes the article moment actually needs. A single concept can be one focal node with no connector line; a contrast can use two separated nodes; a process, journey, timeline, or argument map can use 3-5 nodes with large whitespace between groups.
- Do not use floating islands, rocky islands, grassland, moss carpets, soil terrain, cliffs, terrain chunks, miniature landscapes, scenic bases, matte-gray platforms, or plinths.
- Small plants, sprouts, leaves, flowers, or botanical icons are allowed when they directly serve the article metaphor or a small story node. Keep them as compact paper-like props or annotated node elements, not as ground, scenery, or a landscape base.
- Supporting marks use sparse hand-drawn connector lines when needed, arrows, circles, colored dots, red underlines, tiny tape tabs, paper scraps, motion strokes, and handwritten notes.
- The overall image should feel like a quiet inline illustration, not a poster, cover image, hero image, decorative spotlight, product render, or complex story spread.
- Default aspect ratio is 16:9.

## Character Reference Rules

Use the selected character reference as the canonical identity and anatomy/structure reference whenever generating images.

Reference priority:

1. User-provided character reference image for the current task.
2. Task-generated `images/character-reference.png` when the user provides a text-only character description.
3. Bundled default `../assets/character-reference.png`, currently the 粉色海星 preset.

Do not use a scene image reference. Scene style must be expressed as prompt text.

- Treat the reference image as an identity lock for the protagonist's silhouette, face, signature details, line weight, colors, rendering mode, and detail density.
- Treat the reference image as a structure lock for the protagonist's body shape, appendage count/type, visible protrusions, and absent body parts.
- Use the reference image to preserve the character, not to copy its square portrait composition. Final images remain 16:9 article illustrations.
- If the reference is a model sheet or multi-view sheet, use it to understand one canonical character. Do not copy the sheet layout or show multiple character views in the final article image unless the user asks.
- Change only action and pose: small body tilt, simple gesture changes, nearby props, and sparse motion marks are allowed.
- Do not let the model invent new anatomy, clothing, accessories, or body shapes to express an action unless those are already part of the reference or explicitly requested by the user.
- If the user only gives a text character prompt, first generate a clean square character reference on a simple background, save it as `images/character-reference.png`, and use that generated reference for all article illustrations in the package.
- If a tool cannot accept local image references, first make the selected reference image visible to the model if possible. If no image reference can be used, do not generate final images by default; disclose that stable character output requires the reference image and proceed with text-only fallback only if the user explicitly accepts drift risk.
- Keep scene style as text-only instructions: resolved background color, small nodes, optional thin black journey lines, annotation scraps, colored dots, red underlines, and handwritten note rhythm.

## Integrated Generation Rules

The reference image is for identity and anatomy only. The final article illustration must be generated as one integrated 16:9 image.

- Do not crop the reference character out of its square canvas and paste it into a separate scene.
- Do not use local image-processing scripts to threshold, alpha-mask, background-remove, segment, shadow, or composite the protagonist separately from the rest of the image.
- Do not repair a failed scene by placing a character cutout on top of paper cards, connector lines, or a background.
- Local image operations are only acceptable when they affect the whole canvas after visual approval, such as copying, renaming, metadata changes, or resizing/cropping the entire final image.
- If the protagonist is wrong, regenerate or edit the whole scene through `image_gen`; do not patch in the character afterward.

Reject a generated output before delivery if it shows any of these defects:

- a visible square or rectangular patch around the protagonist
- a gray, white, or off-background reference-canvas remnant behind the character
- hard-edged mask boundaries, background-removal halos, or pasted-cutout seams
- a separate drop-shadow box that follows the reference image rectangle
- the square reference portrait composition copied into the 16:9 article scene
- a rough contact sheet, candidate grid, or temporary comparison image used as if it were final output

## Character Structure Budget

Do not assume every custom protagonist has two hands and two feet. The safe rule is: first identify the character's own structure, then preserve that exact structure.

Before writing article-image prompts, create a structure budget from the selected reference or from the user's explicit character description:

- protagonist count: usually `exactly one` in each final image
- body/silhouette: main shape, head/body separation, view limits, and whether the body can tilt
- signature details: face, markings, colors, clothing, accessories, or surface details already present
- appendages: exact count/type of arms, hands, legs, feet, wings, ears, tail, wheels, tentacles, antennae, horns, or other protrusions; write `none` for absent parts
- rendering mode: flat 2D, soft 3D, line art, clay-like, sticker, vector, etc.
- action limits: which actions are safe and which would require new anatomy

Examples of valid custom budgets:

- cloud icon mascot: one rounded cloud body, face on front, appendages = none, no arms or feet, action through floating position, nearby props, and detached motion marks
- snake mascot: one continuous curved body, face at head, appendages = none unless the reference shows them, no feet, action through body curve and nearby nodes
- robot mascot with wheels: one head/body, two simple arms if visible, wheel base instead of feet, no shoes or toes
- winged mascot: two wings as the primary appendages, no extra arms unless visible in the reference
- octopus mascot: use the visible/intended tentacle count from the reference, do not add human hands or feet

If the reference has ambiguous or hidden parts, do not invent them for action. Keep the action in scene props, node layout, arrows, detached motion marks, and small body orientation changes. If the reference contains multiple unrelated characters and the user did not choose one, ask which protagonist to use before final generation.

For text-defined characters, generate the task-level reference with a simple, readable anatomy first. If the user's description specifies a nonstandard body, preserve it. If the description does not specify appendages, pick a minimal structure that fits the character concept, then lock that structure in subsequent prompts.

For every article-image prompt, include both:

```text
Character structure budget: [exact protagonist count, body/silhouette, signature details, appendage count/type, absent parts, rendering mode, unsafe actions].
Pose budget for this image: [how each existing part is positioned], [which props/motion marks are detached], [what must not be added].
```

Write the structure and pose budgets directly into the generation prompt. Do not add a separate character-redesign loop for normal execution, but do run a final visual acceptance check for integration artifacts before delivery. If the image shows a rectangular character patch, mask halo, pasted shadow, copied reference-canvas composition, or other cutout-composite artifact, reject it instead of listing it as a final file.

## Background Color Rules

- Default to exact `#F4F4F2` only when the user does not specify a background color.
- If the user specifies a hex color, use it exactly.
- If the user specifies a named color, choose a stable hex value, state the chosen value in the plan, and reuse it in every prompt and guide entry.
- Prefer a flat or near-flat background. Do not introduce gradients, textures, patterns, or scenery unless the user explicitly asks.
- Keep enough contrast for the character and objects to read clearly, but avoid saturated or high-contrast backgrounds that make the image feel like a poster.

## Composition and Density

- Choose the scene structure from the source:
  - `single-node focus`: one compact object cluster, paper card, small prop, or character action with nearby annotations; no connector line needed.
  - `two-node contrast`: two separated nodes with optional arrow or connector if the relationship needs it.
  - `multi-node journey`: 3-5 nodes arranged left-to-right with a thin hand-drawn connector line only for process, timeline, causality, or step-by-step ideas.
- Keep nodes small and separated: one object cluster, paper card, small prop, or character action per node.
- Keep the background clean and low contrast. Do not fill it with scenery, architecture, UI panels, labels, crowds, or decorative clutter.
- Use very soft, low-opacity shadows under cutout-like props so they feel placed on paper without becoming heavy product renders.
- Keep color saturation gentle and contrast low. The illustration should support reading instead of becoming the page's visual center.
- Keep object scale modest: avoid oversized props, dramatic camera angles, strong foreground objects, scenic base details, and heavy 3D rendering.
- Prefer small, clear metaphors and annotated sequences over rich world-building.

## Character Direction

The protagonist should be cute, clear, and active, but the character design must stay locked across images.

For a custom reference character:

- Preserve the reference character's silhouette, face, signature markings, primary colors, line style, rendering mode, and detail density.
- Preserve the reference character's own appendage count/type and absent parts. Do not force any bundled preset's anatomy onto it.
- Express action through small pose shifts, nearby props, motion marks, and simple gestures.
- Do not redesign the character between images.
- Do not add new costume pieces, props attached to the body, limbs, facial features, or accessories unless the user asks.
- Keep connector lines, arrows, strings, tape, tools, bags, signs, and motion marks visually detached from the body unless they are part of the original reference.

For a text-defined custom character:

- First turn the text prompt into a square reference image with a simple full-body or clear mascot view.
- Keep the reference simple enough to reproduce consistently in small inline illustrations.
- Prefer a compact character with clear silhouette, few colors, and identifiable signature details.
- Avoid over-detailed characters that will drift across multiple images.
- After generating the reference, use it as the structure source before making any article illustrations.

For the bundled default 粉色海星 preset, use these stricter lock rules:

- Rendering: soft 2D sticker/vector illustration with gentle inner shading and subtle glossy highlights. Do not turn the character into a realistic sea star photo, hard 3D sculpture, clay model, plush toy, or underwater creature render.
- Body: one fixed compact five-point rounded starfish body, upright front or slight 3/4 front view, with five soft arms as part of the body silhouette. Keep the same smooth star shape across the image set; do not use side-profile, crawling, kneeling, stretched, squashed, or asymmetrical redesigns.
- Detail level: keep the same soft pink fill, darker pink outline, pale raised dot details, and a few small pink freckles. Do not add dense pores, realistic marine texture, suction cups, spines, scales, shells, or complex shading.
- Face: two glossy dark oval eyes with white highlights, small smiling mouth, and soft pink blush cheeks. Do not add eyebrows, large mouths, teeth, detailed expressions, changed eye style, or extra facial features.
- Appendages: the five starfish arms are the only body protrusions and are part of the silhouette, not separate hands or feet. Do not add human arms, hands, fingers, legs, shoes, toes, tentacles, wings, tail, or extra star points.
- Action: express movement through slight body tilt, position changes, nearby props, detached motion marks, and scene-node movement. Do not make the starfish grip, carry, point with fingers, kneel, crawl, or use props fused to the body.
- Do not add hair, hats, clothes, gloves, sleeves, realistic limbs, elbows, long arms, human hands, or changing body shapes.

## Text Rules

- Use little or no visible text by default.
- Prefer visual metaphor, objects, gesture, composition, colored dots, underline marks, and optional connector lines over labels.
- If text is useful, make it look handwritten: short note-like Chinese or English words, pencil/marker style, slightly imperfect, integrated as small annotations above or beside story nodes.
- Keep handwritten text short. A typical image can use 2-5 labels, each usually 2-8 Chinese characters or 1-4 English words.
- Avoid paragraphs, dense captions, long UI labels, printed typography, and text-heavy diagrams.

## Scene Planning

Each image must answer:

1. What article moment does this image support?
2. Which character reference and character name are being used?
3. What exact background color is being used?
4. What is the reference-derived character structure budget?
5. Is this a small story moment or a single explanatory image?
6. What is the protagonist doing, and does that action stay inside the structure budget?
7. How does the prompt keep the protagonist's identity and anatomy/structure consistent with the selected reference?
8. Does this article moment need a `single-node focus`, `two-node contrast`, or `multi-node journey`?
9. If it is a journey or contrast, what thin hand-drawn connector line or arrows clarify the relationship? If it is a single node, what tape tabs, colored dots, red underlines, or note scraps clarify the idea without a connector line?
10. What parts of the image are cutout-like/soft 3D, and how does the protagonist remain consistent with the reference?
11. Does the composition keep at least 55% empty background?
12. What can be removed so the image stays light enough for article reading?
13. What sparse handwritten short labels help the reader without becoming dense text?

Use a multi-node story when the article has process, change, discovery, conflict, or emotion. Use a single-node explanatory image when the article needs one clear concept, object, quote, comparison anchor, or summary.

## Prompt Pattern

Use this structure when writing image prompts:

```text
Create a quiet, low-visual-weight 16:9 inline illustration for [article placement/purpose]. The article text must remain the visual priority.
Input image/reference: use [selected reference path] as the identity reference for [character name]. Preserve the reference character's silhouette, face, signature details, colors, line style, rendering mode, and detail density. Use only the character identity from the reference; do not copy the square portrait composition. Change only [character name]'s action/pose for this scene.
Integrated generation: generate the whole 16:9 article scene as one image. Do not crop, alpha-mask, background-remove, paste, shadow, or locally composite the protagonist from the reference image. No visible square/rectangular patch, gray or white canvas remnant, hard mask edge, background-removal halo, separate drop-shadow box, or copied reference portrait may appear around the character.
Character structure budget: [protagonist count; body/silhouette; signature details; exact appendage count/type including arms/hands/legs/feet/wings/tail/wheels/tentacles/antennae/other protrusions; explicitly absent parts; rendering mode; unsafe actions]. This budget comes from the selected reference or the user's explicit description, not from an unrelated bundled preset.
Pose budget for this image: [describe how each existing body part/appendage is positioned for this scene]. Keep props, connector lines, arrows, strings, tape, tools, signs, and motion marks detached from the body unless they exist in the reference. Do not add absent parts or extra appendages for action.
Scene style: text-only annotated-node/storyboard style, with small separated object nodes, optional thin hand-drawn black connector line, tape scraps, colored dots, red underlines, and sparse handwritten annotations.
Background: exact fixed color [resolved background hex], clean and calm, with no full-frame scenery and no background variation between images.
Scene structure: [single-node focus / two-node contrast / multi-node journey], chosen to match the article moment.
Scene: [one specific focal node / two specific contrast nodes / 3-5 specific journey nodes]. Use connector lines only if the selected structure needs sequence, movement, comparison, causality, or a journey. Use small cutout-like objects, paper cards, tape tabs, colored dots, and red underlines with very soft low-opacity shadows.
Style split: objects, paper scraps, tape, lighting, and shadows can be cutout-like or soft 3D; [character name] keeps the rendering style and identity from the selected reference image.
Character: [character name] matches the selected reference image across every image in the set. [If default 粉色海星 preset: exactly one compact five-point rounded pink starfish silhouette, upright front or slight 3/4 front view, soft 2D sticker/vector rendering, darker pink outline, pale raised dot details, glossy dark oval eyes with white highlights, small smiling mouth, soft blush cheeks, five starfish arms as body protrusions, no separate hands, no separate feet, no human limbs, and no extra or missing star points.] [character name] is [specific action and emotion], expressed through a small pose/action change, tiny prop, small body tilt, or detached motion marks without changing identity or structure.
Doodles: sparse hand-drawn connector lines only when needed, plus arrows, circles, motion marks, colored dots, red underlines, and tape marks around the node or nodes.
Text: [none / 2-5 very short handwritten note labels].
Mood: [specific tone matching the article].
Composition: at least 55% calm negative space, small separated node(s), low contrast and low saturation, very soft shadows, low visual weight suitable for an article body.
Avoid: dense text, printed typography, busy full-frame environment, complex city, crowded desk, many objects, many characters, floating island, rocky island, grassland, moss carpet, soil terrain, cliffs, stones, terrain chunks, miniature landscape, matte-gray platform, plinth, oversized props, dramatic perspective, strong shadows, saturated colors, poster-like contrast, cover image, hero image, decorative spotlight, plain mascot portrait, generic stock image, arbitrary character redesign, new anatomy not present in the reference, extra or missing appendages, hidden/back duplicated limbs, body-attached motion marks that read as limbs, props fused to the body, new clothing/accessories unless requested, inconsistent identity across images, visible square/rectangular patches around the protagonist, gray/white pasted canvas remnants, hard mask edges, background-removal halos, separate cutout shadows, or locally composited character stickers. Small paper-like sprouts, leaves, flowers, potted plants, and botanical icons are allowed as compact story nodes when relevant; do not turn them into scenery or a base.
```
