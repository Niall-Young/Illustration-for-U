# 小饭团视觉风格参考

## Core Style

- 小饭团 is a flat 2D illustrated rice-ball character placed inside the image as an expressive story actor.
- The environment is a minimal realistic 3D isometric floating island with physical depth, believable lighting, and a few tactile objects.
- The style split is intentional: the island, props, lighting, and shadows are 3D; 小饭团 is a 2D line-and-fill illustration that sits inside the 3D scene like a sticker or drawn character.
- The canvas should start from a shallow light gray background, such as `#f3f4f6`, `#f4f4f2`, or another soft neutral gray.
- The floating island should feel small and airy, usually occupying about 35-50% of the 16:9 frame, with calm negative space around it.
- Supporting marks use sparse hand-drawn doodle lines, arrows, sparkles, motion strokes, circles, and small annotation marks.
- The overall image should feel like a quiet article illustration: a tiny real-world diorama that a 2D character has entered, not a poster, cover image, or complex story spread.
- Default aspect ratio is 16:9.

## Composition and Density

- Use one main floating island per image. One or two tiny satellite pieces are allowed only when they clarify the article idea.
- Limit the scene to one main idea and 3-5 supporting props at most.
- Keep the background clean and low contrast. Do not fill it with scenery, architecture, UI panels, labels, crowds, or decorative clutter.
- Use soft shadows beneath the island to show that it is floating.
- Keep color saturation gentle. The illustration should support reading instead of becoming the page's visual center.
- Prefer small, clear metaphors over rich world-building.

## Character Direction

小饭团 should be cute, curious, and active, but the character design must stay stable across images.

Character lock:

- Rendering: flat 2D illustration only, with clean line art and simple color fills. Do not give 小饭团 3D volume, realistic material, sculpted rice grains, 3D lighting, or 3D cast shadows.
- Body: a small rounded triangular rice-ball body, soft white or warm off-white, with only subtle flat drawn rice-grain marks if needed.
- Face: two simple dark dot eyes, tiny blush marks if useful, and a very small mouth only when needed for expression.
- Seaweed: one fixed dark green or charcoal nori patch on the lower front of the body.
- Arms: two short rounded dark charcoal line arms attached at the middle-left and middle-right sides. Keep them simple, noodle-like, and fingerless.
- Hands: if an object must be held, use tiny rounded mitten-like ends only; do not add fingers.
- Feet: no legs by default; two tiny dark oval feet are allowed only when walking or balancing.
- Do not add hair, hats, clothes, gloves, sleeves, realistic limbs, elbows, long arms, human hands, 3D body shading, or changing body shapes.

Give the character a concrete action in every image, using the fixed arm style, such as:

- stepping across a small floating island
- holding a tiny magnifying glass over one key detail
- gently pushing a small object into place
- pointing at a turning point with one short line arm
- arranging two or three objects on the island
- climbing, observing, collecting, sorting, comparing, or celebrating

Do not leave 小饭团 standing passively unless the scene itself is intentionally quiet.

## Text Rules

- Use little or no visible text by default.
- Prefer visual metaphor, objects, gesture, composition, and doodle marks over labels.
- If text is useful, make it look handwritten: short note-like Chinese or English words, pencil/marker style, slightly imperfect, integrated as a small annotation beside the floating island.
- Keep handwritten text to one or two very short phrases, usually 2-6 Chinese characters or 1-3 English words each.
- Avoid paragraphs, dense captions, long UI labels, printed typography, and text-heavy diagrams.

## Scene Planning

Each image must answer:

1. What article moment does this image support?
2. Is this a small story moment or a single explanatory image?
3. What is 小饭团 doing?
4. What parts of the image are 3D, and how does 小饭团 remain clearly 2D?
5. What small floating island surrounds 小饭团?
6. What can be removed so the image stays light enough for article reading?
7. What sparse doodle marks or handwritten short text help the reader?

Use a small story when the article has process, change, discovery, conflict, or emotion. Use a single explanatory image when the article needs a clear concept, object, comparison, or summary.

## Prompt Pattern

Use this structure when writing image prompts:

```text
Create a 16:9 illustration for [article placement/purpose].
Background: shallow light gray, clean and calm, with no full-frame scenery.
Scene: one small realistic 3D isometric floating island, occupying about 35-50% of the frame, with [3-5 specific objects] and soft shadow beneath the island.
Style split: the island, props, lighting, and shadows are 3D; 小饭团 is a flat 2D line-and-fill illustration, like a sticker character placed into the 3D scene.
Character: 小饭团 uses the fixed 2D design: small rounded triangular off-white rice-ball silhouette, simple flat fill, optional subtle drawn rice-grain marks, two dark dot eyes, one fixed dark nori patch on the lower front, two short rounded dark charcoal line arms with no fingers, no 3D body shading, no clothes or changing limbs. 小饭团 is [specific action and emotion].
Doodles: sparse hand-drawn lines, arrows, sparkles, motion marks, circles, or handwritten short notes around only the most important supporting elements.
Text: [none / one or two short handwritten note phrases].
Mood: [specific tone matching the article].
Composition: calm negative space around the island, one focal point, low visual weight suitable for an article body.
Avoid: dense text, printed typography, busy full-frame environment, complex city, crowded desk, many objects, many characters, poster-like contrast, plain mascot portrait, generic stock image, 3D 小饭团, realistic rice sculpture, changing 小饭团 body shape, long arms, fingers, gloves, sleeves, or realistic limbs.
```
