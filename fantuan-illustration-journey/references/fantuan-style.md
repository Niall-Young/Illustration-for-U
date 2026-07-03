# 小饭团视觉风格参考

## Core Style

- 小饭团 is a flat 2D illustrated rice-ball character placed inside the image as an expressive story actor.
- The environment is a clean whiteboard annotated-node/storyboard: one or more small cutout-like objects and story nodes on the exact fixed `#F4F4F2` canvas. Use thin hand-drawn black lines or arrows only when the article moment needs sequence, movement, comparison, causality, or a journey.
- The style split is intentional: objects, paper scraps, tape tabs, lighting, and shadows can be cutout-like or soft 3D; 小饭团 is a 2D line-and-fill illustration that sits inside the whiteboard scene like a sticker or drawn character.
- The canvas must use the fixed shallow light gray background `#F4F4F2`. Do not vary the background gray between images in the same package.
- Use the number of visual nodes the article moment actually needs. A single concept can be one focal node with no connector line; a contrast can use two separated nodes; a process, journey, timeline, or argument map can use 3-5 nodes with large whitespace between groups.
- Do not use floating islands, rocky islands, grass, moss, soil, cliffs, terrain chunks, stones, plants, miniature landscapes, scenic bases, matte-gray platforms, or plinths.
- Supporting marks use sparse hand-drawn connector lines when needed, arrows, circles, colored dots, red underlines, tiny tape tabs, paper scraps, motion strokes, and handwritten notes.
- The overall image should feel like a quiet inline visual essay or annotated whiteboard scene, not a poster, cover image, hero image, decorative spotlight, product render, or complex story spread.
- Default aspect ratio is 16:9.

## Locked Reference Asset

Use `../assets/fantuan-character-reference.png` as the canonical Image Gen-created mascot identity reference whenever generating images.
Do not use a scene image reference. Scene style must be expressed as prompt text.

- Treat the PNG as an identity lock for 小饭团's body, face, nori patch, 小黑线手, 小黑线脚, line weight, colors, and flat 2D rendering.
- Use the reference image to preserve the mascot, not to copy its square portrait composition. Final images remain 16:9 article illustrations.
- Change only action and pose: small body tilt, short arm angle, nearby props, and sparse motion marks are allowed.
- Do not let the model invent new hands, fingers, filled feet, legs, clothing, accessories, or body shapes to express an action.
- If the PNG is missing or visibly unsuitable, generate a new fixed square mascot reference with Image Gen first and save it back to `../assets/fantuan-character-reference.png`.
- If a tool cannot accept local image references, first make the PNG visible to the model if possible. If no image reference can be used, do not generate final images by default; disclose that stable mascot output requires the reference image and proceed with text-only fallback only if the user explicitly accepts drift risk.
- Keep scene style as text-only instructions: exact `#F4F4F2` background, small nodes, optional thin black journey lines, annotation scraps, colored dots, red underlines, and handwritten note rhythm.

## Composition and Density

- Choose the scene structure from the source:
  - `single-node focus`: one compact object cluster, paper card, small prop, or 小饭团 action with nearby annotations; no connector line needed.
  - `two-node contrast`: two separated nodes with optional arrow or connector if the relationship needs it.
  - `multi-node journey`: 3-5 nodes arranged left-to-right with a thin hand-drawn connector line only for process, timeline, causality, or step-by-step ideas.
- Keep nodes small and separated: one object cluster, paper card, small prop, or 小饭团 action per node.
- Keep the background clean and low contrast. Do not fill it with scenery, architecture, UI panels, labels, crowds, or decorative clutter.
- Use very soft, low-opacity shadows under cutout-like props so they feel placed on paper without becoming heavy product renders.
- Keep color saturation gentle and contrast low. The illustration should support reading instead of becoming the page's visual center.
- Keep object scale modest: avoid oversized props, dramatic camera angles, strong foreground objects, scenic base details, and heavy 3D rendering.
- Prefer small, clear metaphors and annotated sequences over rich world-building.

## Character Direction

小饭团 should be cute, curious, and active, but the character design must stay locked across images. Treat `../assets/fantuan-character-reference.png` as the fixed mascot sheet: action can change, anatomy cannot.

Character lock:

- Rendering: flat 2D illustration only, with clean line art and simple color fills. Do not give 小饭团 3D volume, realistic material, sculpted rice grains, 3D lighting, or 3D cast shadows.
- Body: one fixed compact rounded triangular rice-ball body, soft white or warm off-white, width about 85-95% of height, upright front or slight 3/4 front view. Keep the same smooth silhouette across the image set; do not use side-profile, crawling, kneeling, stretched, squashed, or leaning-body redesigns.
- Detail level: at most 2-3 subtle flat rice-grain marks. Keep line weight and detail density consistent across images. Do not add realistic rice texture, extra contour lines, complex shading, or different surface detail from image to image.
- Face: two simple dark dot eyes in the same style and spacing, tiny blush marks if useful, and a very small mouth only when needed for expression. Do not add eyebrows, large mouths, detailed expressions, changed eye shapes, or extra facial features.
- Seaweed: one fixed dark green or charcoal nori patch on the lower front of the body, centered, rounded-rectangle-like, about one-third of body height. It is part of the mascot body, not clothing, a bag, a shadow, or a movable prop. Keep its position and scale consistent.
- Hands/arms: two short rounded dark charcoal line strokes attached at the middle-left and middle-right sides, like 小黑线手. Keep them simple, noodle-like, fingerless, and short, about 20-30% of body width. Do not draw long reaching arms, elbows, sleeves, gloves, human hands, index fingers, separated fingers, circular hands, mittens, or detailed hand poses.
- Feet: exactly two tiny dark charcoal curved line strokes tucked directly under the body, like 小黑线脚. Each foot is a short rounded-cap line only. Do not draw filled oval blobs, shoes, toes, stick legs, long thin legs, crawling legs, kneeling legs, separated line legs, or feet extending far from the body.
- Do not add hair, hats, clothes, gloves, sleeves, realistic limbs, elbows, long arms, human hands, 3D body shading, or changing body shapes.

Pose rules:

- Keep 小饭团 upright in a front or slight 3/4 front view by default.
- Express action through short black line hands/arms, two tiny black line feet, tiny props, a small body tilt, or nearby motion marks.
- Do not change anatomy to fit an action. Avoid crawling, kneeling, sitting with extended legs, running with long legs, side-profile posing, or large gesture poses.

Give the character a concrete action in every image, using the fixed arm style, such as:

- standing beside a single annotated node
- walking along a hand-drawn connector line when the scene is a journey
- holding a tiny magnifying glass over one key detail
- gently pushing a small object into place
- pointing at a turning point with one short black line arm
- arranging two or three objects as a story node
- adding tape to a tiny note card
- marking a node with a red underline or colored dot
- observing, collecting, sorting, comparing, or celebrating with small props and short arms

Do not leave 小饭团 standing passively unless the scene itself is intentionally quiet.

## Text Rules

- Use little or no visible text by default.
- Prefer visual metaphor, objects, gesture, composition, colored dots, underline marks, and optional connector lines over labels.
- If text is useful, make it look handwritten: short note-like Chinese or English words, pencil/marker style, slightly imperfect, integrated as small annotations above or beside story nodes.
- Keep handwritten text short. A typical image can use 2-5 labels, each usually 2-8 Chinese characters or 1-4 English words.
- Avoid paragraphs, dense captions, long UI labels, printed typography, and text-heavy diagrams.

## Scene Planning

Each image must answer:

1. What article moment does this image support?
2. Is this a small story moment or a single explanatory image?
3. What is 小饭团 doing?
4. How does the prompt keep 小饭团's body, face, nori patch, short black line hands/arms, two tiny black line feet, and low detail level identical across images?
5. Does this article moment need a `single-node focus`, `two-node contrast`, or `multi-node journey`?
6. If it is a journey or contrast, what thin hand-drawn connector line or arrows clarify the relationship? If it is a single node, what tape tabs, colored dots, red underlines, or note scraps clarify the idea without a connector line?
7. What parts of the image are cutout-like/soft 3D, and how does 小饭团 remain clearly 2D?
8. Does the composition keep at least 55% empty `#F4F4F2` background?
9. What can be removed so the image stays light enough for article reading?
10. What sparse handwritten short labels help the reader without becoming dense text?

Use a multi-node story when the article has process, change, discovery, conflict, or emotion. Use a single-node explanatory image when the article needs one clear concept, object, quote, comparison anchor, or summary.

## Prompt Pattern

Use this structure when writing image prompts:

```text
Create a quiet, low-visual-weight 16:9 inline illustration for [article placement/purpose]. The article text must remain the visual priority.
Input image/reference: use assets/fantuan-character-reference.png as the identity reference for 小饭团. Preserve the reference mascot's silhouette, face, nori patch, line weight, short rounded black line hands/arms, two tiny black curved line feet, colors, and flat 2D rendering. Use only the mascot identity from the reference; do not copy the square portrait composition. Change only 小饭团's action/pose for this scene.
Scene style: text-only whiteboard annotated-node style, with small separated object nodes, optional thin hand-drawn black connector line, tape scraps, colored dots, red underlines, and sparse handwritten annotations.
Background: exact fixed color #F4F4F2, clean and calm, with no full-frame scenery and no background variation between images.
Scene structure: [single-node focus / two-node contrast / multi-node journey], chosen to match the article moment.
Scene: [one specific focal node / two specific contrast nodes / 3-5 specific journey nodes]. Use connector lines only if the selected structure needs sequence, movement, comparison, causality, or a journey. Use small cutout-like objects, paper cards, tape tabs, colored dots, and red underlines with very soft low-opacity shadows.
Style split: objects, paper scraps, tape, lighting, and shadows are cutout-like or soft 3D; 小饭团 is a flat 2D line-and-fill illustration, like a sticker character placed into the whiteboard scene.
Character: 小饭团 uses the loaded reference image as the locked fixed 2D mascot design and must match across every image in the set: compact rounded triangular off-white rice-ball silhouette, upright front or slight 3/4 front view, width about 85-95% of height, simple flat fill, at most 2-3 subtle flat rice-grain marks, two small dark dot eyes, optional tiny mouth only, one fixed dark green-charcoal rounded nori patch centered on the lower front about one-third of body height, two short rounded dark charcoal line hands/arms attached to body sides with no fingers and no elbows, and exactly two tiny dark charcoal curved line feet tucked directly under the body. 小饭团 is [specific action and emotion], expressed through short black line hands/arms, tiny black line feet, a tiny prop, small body tilt, or motion marks without changing anatomy.
Doodles: sparse hand-drawn connector lines only when needed, plus arrows, circles, motion marks, colored dots, red underlines, and tape marks around the node or nodes.
Text: [none / 2-5 very short handwritten note labels].
Mood: [specific tone matching the article].
Composition: at least 55% calm negative space, small separated node(s), low contrast and low saturation, very soft shadows, low visual weight suitable for an article body.
Avoid: dense text, printed typography, busy full-frame environment, complex city, crowded desk, many objects, many characters, floating island, rocky island, grass, moss, soil, cliffs, plants, stones, terrain chunks, miniature landscape, matte-gray platform, plinth, oversized props, dramatic perspective, strong shadows, saturated colors, poster-like contrast, cover image, hero image, decorative spotlight, plain mascot portrait, generic stock image, 3D 小饭团, realistic rice sculpture, side-profile 小饭团, crawling pose, kneeling pose, sitting with extended legs, running with long legs, changing 小饭团 body shape, stretched body, squashed body, long arms, elbows, fingers, pointing hands, circular hands, mittens, gloves, sleeves, filled oval feet, shoes, toes, stick legs, long thin legs, separated line legs, clothing, accessories, hair, hats, or realistic limbs.
```
