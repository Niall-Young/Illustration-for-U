---
name: illustration-for-u
description: "Create configurable article/material illustration packages. Use when the user asks in Chinese or English to 给文章配图, 给这篇文章做插图/配图, 按文章结构生成一组图, 为正文插图, 用我的角色做配文插画, 把这个形象作为文章插画主角, 替换默认角色, 换背景色, create article illustrations, make images for an article, use my character as the article illustration mascot, replace the default character, or turn pasted text/Markdown/PRDs/campaign materials into inline illustrations. Trigger before generic imagegen: read the source, choose placement anchors, resolve the character from the user's reference image, text prompt, or default assets/character-reference.png pink starfish preset, encode that character's own structure limits in prompts instead of assuming two hands/two feet, resolve background color or default #F4F4F2, apply quiet annotated-node/storyboard rules, generate each final 16:9 scene directly with image_gen instead of local cutout compositing, reject rectangular/masked/pasted-character artifacts, and produce images/ plus guide.md."
---

# Illustration for U

## Overview

Use this skill to turn an article, document, PRD, content draft, campaign material, or pasted text into a complete illustration package: planned insertion points, generated images, and a Markdown guide explaining where to place each image.

Always read `references/illustration-style.md` before writing image prompts or final placement guidance. Use `image_gen` only as the downstream generation tool. Do not replace this skill's article reading, placement planning, character/background configuration, prompt planning, file naming, or guide-writing workflow with a generic image generation flow.

Default visual direction: quiet supporting illustrations for articles, not cover art, posters, decorative hero images, or full-scene key visuals. The article is the main content; illustrations must feel like small inline visual essays that support reading without competing for attention.

## Configuration Rules

Resolve these before planning images:

- Character:
  - If the user provides a character reference image, use that image as the identity reference.
  - If the user provides a text-only character description, first generate a stable square character reference image for this task, save it as `images/character-reference.png`, then use it as the identity and structure reference for all article illustrations.
  - If the user does not provide a custom character, use the bundled default `assets/character-reference.png`. The bundled preset is 粉色海星.
  - If the user asks to permanently change this skill's default character, replace `assets/character-reference.png` and update the preset notes in `references/illustration-style.md`.
- Character name:
  - Use the user's provided name when available.
  - Use `粉色海星` only for the bundled default preset.
  - Use `主角` or a concise generated name only when the user provides a custom unnamed character.
- Background color:
  - Use the user's requested exact color when provided, including hex values or a clear named color.
  - If the user gives a named color, choose a stable hex value and state it in the plan.
  - If no background color is provided, use the default `#F4F4F2`.
  - Keep the same background color across every image in the package unless the user explicitly asks for per-image variation.

Do not force the bundled preset anatomy onto a custom character. For custom characters, lock the supplied or generated reference's own silhouette, face, signature details, colors, line style, and detail density.

Also do not assume custom characters have two hands and two feet. Some user-provided characters may be a cloud, snake, seal, robot, abstract icon, wheel-based mascot, many-legged creature, winged mascot, or no-limb symbol. Derive the anatomy/structure budget from the selected reference or from the user's explicit description, then preserve that budget across the whole package.

## Reference-Image Workflow

- Before the first `image_gen` call, load, view, or attach the selected character reference image so the image generation step can see it.
- If the selected reference is a model sheet or multi-view image, use it as identity/anatomy guidance only. Do not copy the sheet layout, multiple views, or multiple character copies into the final article illustration.
- In every image prompt, explicitly say that the selected reference image is the identity and anatomy/structure reference and that only pose/action may change.
- In every image prompt, state the resolved background color exactly.
- In every image prompt, state the scene style as text: clean annotated-node/storyboard composition, small object clusters, optional hand-drawn connector lines, paper/tape details, colored dots, red underlines, and sparse handwritten notes.
- Do not ask image generation to invent the character from text alone when a reference image can be supplied or made visible.
- Do not copy the square reference-canvas composition into the article illustration. Use only the character identity and structure from the reference; the final illustration must still be a 16:9 article scene.
- Keep one consistent protagonist across the image set. Do not reproduce multiple reference-sheet copies unless the user explicitly asks for multiple characters.
- If image generation cannot use or see the selected character reference, do not generate final images by default. Produce the illustration plan and explain that stable character output requires the reference image; proceed with text-only fallback only if the user explicitly accepts the drift risk.

## Integrated-Image Rule

Final article illustrations must be complete generated scenes, not local composites.

- Use the selected character reference as an identity/anatomy input or visible reference for `image_gen`.
- Do not crop, segment, threshold, alpha-mask, background-remove, or paste the reference character into another generated scene with PIL, canvas, SVG, CSS, or any local image-editing script.
- Do not create final scenes by placing a character cutout over paper cards, shadows, connector lines, or backgrounds. That workflow creates visible square canvases, gray/white rectangles, mask halos, and pasted-sticker artifacts.
- Local post-processing is allowed only for whole-canvas file operations after the image has passed visual review: renaming, copying, metadata changes, or resizing/cropping the entire 16:9 image. Do not process the protagonist separately from the rest of the canvas.
- If the character is wrong or the scene needs revision, regenerate or edit the whole illustration through `image_gen`; do not patch the character in afterward.

## Prompt-Time Character Structure Rules

Before writing image prompts, derive a compact character structure budget from the selected reference or the user's explicit description. If the character came from a text-only prompt, generate `images/character-reference.png` first and use that generated reference as the structure source for the rest of the package.

The structure budget must record:

- protagonist count: normally exactly one protagonist in each final image unless the user asks for more
- body/silhouette: main body shape, head/body separation if any, and view limits
- signature identity details: face, markings, colors, clothing or accessories that already exist in the reference
- appendages: exact visible and intended count/type of arms, hands, legs, feet, wings, ears, tail, wheels, tentacles, antennae, or other protrusions; write `none` when absent
- rendering constraints: 2D/3D, line weight, material, detail density, and whether props may touch the body
- unsafe actions: gestures that would require new anatomy, long reach, gripping, fingers, extra legs, copied action frames, or body-attached props

For model sheets or multi-view references, derive the budget from one canonical character, not by counting all repeated views in the sheet. Final article images still show one protagonist unless the user explicitly asks for several characters.

For custom characters with unclear anatomy, use the reference image as the source of truth. If a body part is not visible and not described by the user, do not invent it for action. Prefer simple pose changes, nearby props, detached motion marks, and scene-node movement over adding limbs. If the reference contains multiple unrelated characters and the user has not chosen one, stop and ask which character to use before generating final images.

For the bundled default 粉色海星 preset, the structure budget is stricter: exactly one five-point rounded pink starfish body, glossy dark eyes, small smiling mouth, pink blush cheeks, raised pale pink dot details, darker pink outer outline, five starfish arms that are part of the body silhouette, no separate hands, no separate feet, no human limbs, no clothing, no accessory drift, and no extra or missing star points.

For each image prompt, include a short pose budget:

```text
character structure budget: ...
pose budget: left-side part = ..., right-side part = ..., lower parts = ..., other protrusions = ...
detached marks/props: ...
```

Adapt the pose-budget labels to the actual character. A snake may have `arms = none` and `feet = none`; a cloud icon may have `appendages = none`; a robot may have two arms and wheels; an octopus may have the visible tentacle count from the reference. Do not rewrite these into a different preset's anatomy rules unless that preset is actually being used.

In every generation prompt, restate only the prompt-relevant structure and pose constraints. Keep connector lines, motion marks, arrows, red underlines, strings, tape, tools, and props visibly detached from the character's body unless they are part of the original reference. If an article moment seems to need complex gripping, carrying, climbing, crawling, or multiple action frames, move the action into nearby props, annotations, node layout, or a connector path instead of changing the character's anatomy.

## Workflow

1. Read the full source material before planning images.
2. Resolve character, character name, and background color.
3. If the character is text-only, generate `images/character-reference.png` first and use it as the reference for the rest of the package.
4. Derive a compact character structure budget from the selected character reference or explicit description.
5. Identify the best places for illustrations:
   - Prefer major section openings, important concept transitions, examples, summaries, or emotional beats.
   - Do not create an image for every paragraph.
   - Merge nearby ideas into one illustration when they serve the same reader need.
6. Create an image plan before generating article illustrations. For each planned image, specify:
   - placement anchor: heading, paragraph summary, quote, or nearby text
   - image purpose: what the reader should understand or feel
   - scene/story: whether this is a small story moment or a single explanatory image
   - character action: what the protagonist is doing in the scene
   - character reference use: which reference image is used and how only the action/pose changes
   - character structure budget: the reference-derived body/appendage/signature-detail budget; do not force bundled-preset anatomy onto custom characters
   - pose budget: how each existing body part or appendage is used in this image, plus which motion marks and props remain detached
   - background color: exact resolved color
   - scene prompt use: choose and describe the annotated-node/storyboard scene rules in text; do not use any scene image as a generation reference
   - scene structure: choose `single-node focus`, `two-node contrast`, or `multi-node journey` based on the article moment
   - style split: what objects are cutout-like/soft 3D and how the character remains consistent with the reference
   - visual weight: the one main idea, 1-5 small nodes as needed, at least 55% calm negative space, muted color, and soft shadow level
   - key visual elements: object node(s), optional left-to-right story path, optional connector line, paper scraps/tape tabs, colored dots, red underlines, sparse doodle accents
   - optional handwritten text: short, sparse note-like text only when it improves comprehension
   - alt text
7. Generate each image with `image_gen`:
   - load or attach the selected character reference image as the identity and anatomy/structure reference
   - generate the full article scene as one integrated image; never use local subject cutout, alpha mask, background removal, or paste-over compositing for the final output
   - preserve the character's locked silhouette, appendage budget, face, signature details, colors, line style, and detail density
   - change only the scene-specific action/pose through small gesture changes allowed by the structure budget, a small body tilt, nearby props, and sparse detached motion marks
   - build the scene as an annotated-node/storyboard composition, not a platform, diorama, floating island, cover image, or poster
   - default aspect ratio: `16:9`
   - filename pattern: `illustration-for-u-01.png`, `illustration-for-u-02.png`, incrementing from `01`
   - output directory: `images/`
8. Run the visual acceptance gate before writing `guide.md`:
   - view each final image at full canvas scale and at the character area
   - reject any image with a visible square/rectangular patch around the character, gray or white canvas remnants, hard mask edges, background-removal halos, mismatched drop-shadow boxes, or a pasted-cutout look
   - reject any image where the square reference portrait composition appears inside the 16:9 scene
   - reject temporary contact sheets, rough candidates, or images made by local compositing; do not list them as final outputs
9. Write `guide.md` after all images pass the visual acceptance gate.

## Image Prompt Requirements

Every image prompt must include:

- 16:9 article-illustration composition with the resolved exact background color.
- Use the selected character reference image as an input image / visible reference for the protagonist's identity and anatomy/structure.
- The final result must be one integrated generated scene. Do not paste a cropped character reference into a separate background, and do not leave any square reference-canvas area around the protagonist.
- Preserve the reference character's silhouette, appendage count/type, face, signature details, colors, line style, rendering mode, and detail density.
- A visible character structure budget derived from the reference or explicit user description: protagonist count, body/silhouette, signature details, appendages, rendering constraints, and unsafe actions. Do not add absent body parts for action.
- A visible pose budget for this image using the character's own body parts and appendages, plus detached marks/props. Do not force two arms or two feet unless the selected reference actually has that structure.
- If using the default 粉色海星 preset, preserve the five-point rounded pink starfish silhouette, glossy dark eyes, small smiling mouth, blush cheeks, raised pale dot details, darker pink outline, soft 2D sticker/vector rendering, and the absence of separate hands, feet, or human limbs.
- Describe scene composition in prompt text only: clean background, small object nodes, optional thin hand-drawn black connector lines, tape/paper scraps, colored dots, red underlines, and sparse handwritten notes.
- A storyboard scene with 1-5 small nodes based on the article moment. Each node should be a compact object cluster or tiny story moment, not a platform or island.
- One clear article idea, represented as either a single focal annotated node, a two-node contrast, or a short visual journey.
- Low visual weight: at least 55% calm negative space, muted colors, low contrast, small subject scale, very soft shadows, no dramatic lighting, and no strong foreground object.
- A clear style split: objects, paper scraps, tape, props, lighting, and shadows can be cutout-like or soft 3D; the protagonist should keep the rendering style defined by the reference.
- Hand-drawn black connector lines and arrows are optional. Use them only to express sequence, movement, comparison, causality, or a journey; otherwise use circles, colored dots, red underlines, tape tabs, and light annotation marks around a single node.
- Sparse handwritten note text only when useful; use short note-like labels, not paragraphs.
- A clear action for the protagonist that changes pose/action only, not identity.
- The reason the visual supports its article placement.

Avoid prompt wording or workflows that ask for dense typography, long labels, UI screenshots, generic stock-photo scenes, busy full-frame landscapes, complex cities, crowded desks, many characters, floating islands, rocky islands, grassland, soil terrain, cliffs, terrain chunks, natural landscape bases, matte-gray platforms, plinths, oversized object clusters, dramatic perspective, strong shadows, saturated color, poster-like contrast, a cover/hero image, a plain mascot portrait, arbitrary character redesign between images, new anatomy not present in the reference, extra or missing appendages, hidden/back duplicated limbs, body-attached motion marks that can read as limbs, props fused to the body, action poses that require changing the character structure, visible square or rectangular canvas remnants around the protagonist, gray/white pasted patches, hard-edged masks, background-removal halos, separate cutout shadows, or locally composited character stickers. Small paper-like sprouts, leaves, flowers, potted plants, and botanical icons are allowed as compact story nodes when relevant; do not turn them into scenery or a base.

When using the default 粉色海星 preset, also avoid: realistic sea star photography, hard 3D sculpture, underwater scenery, side-profile body redesign, extra star points, missing star points, human arms, human hands, fingers, mittens, legs, feet, shoes, toes, crawling pose, kneeling pose, clothing, accessories, hair, hats, or realistic limbs.

## Output Contract

Create this structure in the user's requested output location:

```text
images/
  illustration-for-u-01.png
  illustration-for-u-02.png
guide.md
```

If a text-only custom character is used, also create:

```text
images/
  character-reference.png
```

`guide.md` must include one section per image with:

- image file path
- suggested insertion location, preferably anchored by heading, paragraph summary, or quote
- image purpose
- scene/story description
- character name and action
- character reference usage
- character structure prompt constraints
- background color
- scene prompt notes
- final-image acceptance notes
- optional handwritten short text, or `无`
- alt text
- generation prompt summary

## Guide Template

```markdown
# Illustration for U 配图放置说明

## illustration-for-u-01.png

- 图片路径：images/illustration-for-u-01.png
- 建议位置：放在「...」标题下，... 段之前
- 图片用途：...
- 场景/故事：...
- 角色动作：...
- 角色参考：使用 ... 作为身份参考，仅改变动作/姿态
- 角色结构约束：...
- 背景色：...
- 场景提示：使用文字规则描述注释式构图，不加载额外场景图片
- 成片质检：整图一次生成；无角色矩形底、灰白贴片、硬边遮罩、抠图光晕或局部拼贴痕迹
- 可选文字：...
- Alt text：...
- 提示词摘要：...
```

## Output Completion

- All planned images have matching files in `images/`.
- `guide.md` references the exact generated filenames.
- Character, character reference path, and background color are recorded in the plan and `guide.md`.
- `guide.md` summarizes the prompt-time character structure constraints used for each image.
- Final images are integrated whole-scene generations, not local character cutout composites.
- No final image has a visible rectangle around the protagonist, gray/white patch, hard mask edge, background-removal halo, mismatched pasted shadow, copied square reference portrait, or temporary contact-sheet/candidate artifact.
- The final answer lists the image files and the guide path.
