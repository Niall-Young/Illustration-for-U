# Illustration for U Style Reference

## Core Style

- Illustration for U creates quiet inline visual essays for articles, documents, PRDs, and campaign materials.
- The environment is a clean annotated-node/storyboard scene: one or more small cutout-like objects and story nodes on a calm, consistent background. Use thin hand-drawn black lines or arrows only when the article moment needs sequence, movement, comparison, causality, or a journey.
- The default background color is `#F4F4F2`, but a user-specified background color always takes priority. Keep the resolved background color consistent across the whole package unless the user asks for variation.
- The protagonist is a reusable article-illustration character. The bundled preset is 小饭团 in `../assets/character-reference.png`, but users can replace it with their own character reference image or a text-defined character.
- The style split is intentional: objects, paper scraps, tape tabs, lighting, and shadows can be cutout-like or soft 3D; the protagonist keeps the rendering mode, line style, colors, and identity from the selected character reference.
- Use the number of visual nodes the article moment actually needs. A single concept can be one focal node with no connector line; a contrast can use two separated nodes; a process, journey, timeline, or argument map can use 3-5 nodes with large whitespace between groups.
- Do not use floating islands, rocky islands, grass, moss, soil, cliffs, terrain chunks, stones, plants, miniature landscapes, scenic bases, matte-gray platforms, or plinths.
- Supporting marks use sparse hand-drawn connector lines when needed, arrows, circles, colored dots, red underlines, tiny tape tabs, paper scraps, motion strokes, and handwritten notes.
- The overall image should feel like a quiet inline illustration, not a poster, cover image, hero image, decorative spotlight, product render, or complex story spread.
- Default aspect ratio is 16:9.

## Character Reference Rules

Use the selected character reference as the canonical identity reference whenever generating images.

Reference priority:

1. User-provided character reference image for the current task.
2. Task-generated `images/character-reference.png` when the user provides a text-only character description.
3. Bundled default `../assets/character-reference.png`, currently the 小饭团 preset.

Do not use a scene image reference. Scene style must be expressed as prompt text.

- Treat the reference image as an identity lock for the protagonist's silhouette, face, signature details, line weight, colors, rendering mode, and detail density.
- Use the reference image to preserve the character, not to copy its square portrait composition. Final images remain 16:9 article illustrations.
- Change only action and pose: small body tilt, simple gesture changes, nearby props, and sparse motion marks are allowed.
- Do not let the model invent new anatomy, clothing, accessories, or body shapes to express an action unless those are already part of the reference or explicitly requested by the user.
- If the user only gives a text character prompt, first generate a clean square character reference on a simple background, inspect it, and save it as `images/character-reference.png`. Use that generated reference for all article illustrations in the package.
- If a tool cannot accept local image references, first make the selected reference image visible to the model if possible. If no image reference can be used, do not generate final images by default; disclose that stable character output requires the reference image and proceed with text-only fallback only if the user explicitly accepts drift risk.
- Keep scene style as text-only instructions: resolved background color, small nodes, optional thin black journey lines, annotation scraps, colored dots, red underlines, and handwritten note rhythm.

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
- Express action through small pose shifts, nearby props, motion marks, and simple gestures.
- Do not redesign the character between images.
- Do not add new costume pieces, props attached to the body, limbs, facial features, or accessories unless the user asks.

For a text-defined custom character:

- First turn the text prompt into a square reference image with a simple full-body or clear mascot view.
- Keep the reference simple enough to reproduce consistently in small inline illustrations.
- Prefer a compact character with clear silhouette, few colors, and identifiable signature details.
- Avoid over-detailed characters that will drift across multiple images.

For the bundled default 小饭团 preset, use these stricter lock rules:

- Rendering: flat 2D illustration only, with clean line art and simple color fills. Do not give 小饭团 3D volume, realistic material, sculpted rice grains, 3D lighting, or 3D cast shadows.
- Body: one fixed compact rounded triangular rice-ball body, soft white or warm off-white, width about 85-95% of height, upright front or slight 3/4 front view. Keep the same smooth silhouette across the image set; do not use side-profile, crawling, kneeling, stretched, squashed, or leaning-body redesigns.
- Detail level: at most 2-3 subtle flat rice-grain marks. Keep line weight and detail density consistent across images. Do not add realistic rice texture, extra contour lines, complex shading, or different surface detail from image to image.
- Face: two simple dark dot eyes in the same style and spacing, tiny blush marks if useful, and a very small mouth only when needed for expression. Do not add eyebrows, large mouths, detailed expressions, changed eye shapes, or extra facial features.
- Seaweed: one fixed dark green or charcoal nori patch on the lower front of the body, centered, rounded-rectangle-like, about one-third of body height. It is part of the mascot body, not clothing, a bag, a shadow, or a movable prop. Keep its position and scale consistent.
- Hands/arms: two short rounded dark charcoal line strokes attached at the middle-left and middle-right sides, like 小黑线手. Keep them simple, noodle-like, fingerless, and short, about 20-30% of body width. Do not draw long reaching arms, elbows, sleeves, gloves, human hands, index fingers, separated fingers, circular hands, mittens, or detailed hand poses.
- Feet: exactly two tiny dark charcoal curved line strokes tucked directly under the body, like 小黑线脚. Each foot is a short rounded-cap line only. Do not draw filled oval blobs, shoes, toes, stick legs, long thin legs, crawling legs, kneeling legs, separated line legs, or feet extending far from the body.
- Do not add hair, hats, clothes, gloves, sleeves, realistic limbs, elbows, long arms, human hands, 3D body shading, or changing body shapes.

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
4. Is this a small story moment or a single explanatory image?
5. What is the protagonist doing?
6. How does the prompt keep the protagonist's identity consistent with the selected reference?
7. Does this article moment need a `single-node focus`, `two-node contrast`, or `multi-node journey`?
8. If it is a journey or contrast, what thin hand-drawn connector line or arrows clarify the relationship? If it is a single node, what tape tabs, colored dots, red underlines, or note scraps clarify the idea without a connector line?
9. What parts of the image are cutout-like/soft 3D, and how does the protagonist remain consistent with the reference?
10. Does the composition keep at least 55% empty background?
11. What can be removed so the image stays light enough for article reading?
12. What sparse handwritten short labels help the reader without becoming dense text?

Use a multi-node story when the article has process, change, discovery, conflict, or emotion. Use a single-node explanatory image when the article needs one clear concept, object, quote, comparison anchor, or summary.

## Prompt Pattern

Use this structure when writing image prompts:

```text
Create a quiet, low-visual-weight 16:9 inline illustration for [article placement/purpose]. The article text must remain the visual priority.
Input image/reference: use [selected reference path] as the identity reference for [character name]. Preserve the reference character's silhouette, face, signature details, colors, line style, rendering mode, and detail density. Use only the character identity from the reference; do not copy the square portrait composition. Change only [character name]'s action/pose for this scene.
Scene style: text-only annotated-node/storyboard style, with small separated object nodes, optional thin hand-drawn black connector line, tape scraps, colored dots, red underlines, and sparse handwritten annotations.
Background: exact fixed color [resolved background hex], clean and calm, with no full-frame scenery and no background variation between images.
Scene structure: [single-node focus / two-node contrast / multi-node journey], chosen to match the article moment.
Scene: [one specific focal node / two specific contrast nodes / 3-5 specific journey nodes]. Use connector lines only if the selected structure needs sequence, movement, comparison, causality, or a journey. Use small cutout-like objects, paper cards, tape tabs, colored dots, and red underlines with very soft low-opacity shadows.
Style split: objects, paper scraps, tape, lighting, and shadows can be cutout-like or soft 3D; [character name] keeps the rendering style and identity from the selected reference image.
Character: [character name] matches the selected reference image across every image in the set. [If default 小饭团 preset: compact rounded triangular off-white rice-ball silhouette, upright front or slight 3/4 front view, simple flat fill, at most 2-3 subtle flat rice-grain marks, two small dark dot eyes, one fixed dark green-charcoal rounded nori patch centered on the lower front, two short rounded dark charcoal line hands/arms, and exactly two tiny dark charcoal curved line feet tucked directly under the body.] [character name] is [specific action and emotion], expressed through a small pose/action change, tiny prop, small body tilt, or motion marks without changing identity.
Doodles: sparse hand-drawn connector lines only when needed, plus arrows, circles, motion marks, colored dots, red underlines, and tape marks around the node or nodes.
Text: [none / 2-5 very short handwritten note labels].
Mood: [specific tone matching the article].
Composition: at least 55% calm negative space, small separated node(s), low contrast and low saturation, very soft shadows, low visual weight suitable for an article body.
Avoid: dense text, printed typography, busy full-frame environment, complex city, crowded desk, many objects, many characters, floating island, rocky island, grass, moss, soil, cliffs, plants, stones, terrain chunks, miniature landscape, matte-gray platform, plinth, oversized props, dramatic perspective, strong shadows, saturated colors, poster-like contrast, cover image, hero image, decorative spotlight, plain mascot portrait, generic stock image, arbitrary character redesign, new anatomy not present in the reference, new clothing/accessories unless requested, or inconsistent identity across images.
```
