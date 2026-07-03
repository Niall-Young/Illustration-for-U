---
name: illustration-for-u
description: "Create configurable article and material illustration packages for Illustration for U. Use whenever the user asks in Chinese or English to 给文章配图, 给这篇文章做插图/配图, 按文章结构生成一组图, 为正文插图, 用我的角色做配文插画, 把这个形象作为文章插画主角, 替换小饭团角色, 换背景色, create article illustrations, make images for an article, use my character as the article illustration mascot, or turn pasted text/Markdown/PRDs/campaign materials into inline illustrations. Trigger this before generic imagegen: read the source, choose placement anchors, resolve the character config from the user's reference image, text character prompt, or the default assets/character-reference.png 小饭团 preset, resolve the background color from the user's request or default #F4F4F2, apply quiet annotated-node/storyboard scene prompt rules, generate low-visual-weight 16:9 image_gen illustrations, and produce an images/ folder plus guide.md."
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
  - If the user provides a text-only character description, first generate a stable square character reference image for this task, save it as `images/character-reference.png`, inspect it, then use it as the identity reference for all article illustrations.
  - If the user does not provide a custom character, use the bundled default `assets/character-reference.png`. The bundled preset is 小饭团.
  - If the user asks to permanently change this skill's default character, replace `assets/character-reference.png` and update the preset notes in `references/illustration-style.md`.
- Character name:
  - Use the user's provided name when available.
  - Use `小饭团` only for the bundled default preset.
  - Use `主角` or a concise generated name only when the user provides a custom unnamed character.
- Background color:
  - Use the user's requested exact color when provided, including hex values or a clear named color.
  - If the user gives a named color, choose a stable hex value and state it in the plan.
  - If no background color is provided, use the default `#F4F4F2`.
  - Keep the same background color across every image in the package unless the user explicitly asks for per-image variation.

Do not force 小饭团 anatomy onto a custom character. For custom characters, lock the supplied or generated reference's own silhouette, face, signature details, colors, line style, and detail density.

## Reference-Image Workflow

- Before the first `image_gen` call, load, view, or attach the selected character reference image so the image generation step can see it.
- In every image prompt, explicitly say that the selected reference image is the identity reference and that only pose/action may change.
- In every image prompt, state the resolved background color exactly.
- In every image prompt, state the scene style as text: clean annotated-node/storyboard composition, small object clusters, optional hand-drawn connector lines, paper/tape details, colored dots, red underlines, and sparse handwritten notes.
- Do not ask image generation to invent the character from text alone when a reference image can be supplied or made visible.
- Do not copy the square reference-canvas composition into the article illustration. Use only the character identity from the reference; the final illustration must still be a 16:9 article scene.
- Keep one consistent protagonist across the image set. Do not reproduce multiple reference-sheet copies unless the user explicitly asks for multiple characters.
- If image generation cannot use or see the selected character reference, do not generate final images by default. Produce the illustration plan and explain that stable character output requires the reference image; proceed with text-only fallback only if the user explicitly accepts the drift risk.

## Workflow

1. Read the full source material before planning images.
2. Resolve character, character name, and background color.
3. If the character is text-only, generate `images/character-reference.png` first and use it as the reference for the rest of the package.
4. Identify the best places for illustrations:
   - Prefer major section openings, important concept transitions, examples, summaries, or emotional beats.
   - Do not create an image for every paragraph.
   - Merge nearby ideas into one illustration when they serve the same reader need.
5. Create an image plan before generating article illustrations. For each planned image, specify:
   - placement anchor: heading, paragraph summary, quote, or nearby text
   - image purpose: what the reader should understand or feel
   - scene/story: whether this is a small story moment or a single explanatory image
   - character action: what the protagonist is doing in the scene
   - character reference use: which reference image is used and how only the action/pose changes
   - background color: exact resolved color
   - scene prompt use: choose and describe the annotated-node/storyboard scene rules in text; do not use any scene image as a generation reference
   - scene structure: choose `single-node focus`, `two-node contrast`, or `multi-node journey` based on the article moment
   - style split: what objects are cutout-like/soft 3D and how the character remains consistent with the reference
   - visual weight: the one main idea, 1-5 small nodes as needed, at least 55% calm negative space, muted color, and soft shadow level
   - key visual elements: object node(s), optional left-to-right story path, optional connector line, paper scraps/tape tabs, colored dots, red underlines, sparse doodle accents
   - optional handwritten text: short, sparse note-like text only when it improves comprehension
   - alt text
6. Generate each image with `image_gen`:
   - load or attach the selected character reference image as the identity reference
   - preserve the character's locked silhouette, face, signature details, colors, line style, and detail density
   - change only the scene-specific action/pose through small gesture changes, a small body tilt, nearby props, and sparse motion marks
   - build the scene as an annotated-node/storyboard composition, not a platform, diorama, floating island, cover image, or poster
   - default aspect ratio: `16:9`
   - filename pattern: `illustration-for-u-01.png`, `illustration-for-u-02.png`, incrementing from `01`
   - output directory: `images/`
7. Write `guide.md` after all images are ready.

## Image Prompt Requirements

Every image prompt must include:

- 16:9 article-illustration composition with the resolved exact background color.
- Use the selected character reference image as an input image / visible reference for the protagonist's identity.
- Preserve the reference character's silhouette, face, signature details, colors, line style, rendering mode, and detail density.
- If using the default 小饭团 preset, preserve the rounded triangular rice-ball body, small dot eyes, lower-front nori patch, short rounded black line hands/arms, two tiny black curved line feet, simple line weight, and flat 2D rendering.
- Describe scene composition in prompt text only: clean background, small object nodes, optional thin hand-drawn black connector lines, tape/paper scraps, colored dots, red underlines, and sparse handwritten notes.
- A storyboard scene with 1-5 small nodes based on the article moment. Each node should be a compact object cluster or tiny story moment, not a platform or island.
- One clear article idea, represented as either a single focal annotated node, a two-node contrast, or a short visual journey.
- Low visual weight: at least 55% calm negative space, muted colors, low contrast, small subject scale, very soft shadows, no dramatic lighting, and no strong foreground object.
- A clear style split: objects, paper scraps, tape, props, lighting, and shadows can be cutout-like or soft 3D; the protagonist should keep the rendering style defined by the reference.
- Hand-drawn black connector lines and arrows are optional. Use them only to express sequence, movement, comparison, causality, or a journey; otherwise use circles, colored dots, red underlines, tape tabs, and light annotation marks around a single node.
- Sparse handwritten note text only when useful; use short note-like labels, not paragraphs.
- A clear action for the protagonist that changes pose/action only, not identity.
- The reason the visual supports its article placement.

Avoid prompt wording that asks for dense typography, long labels, UI screenshots, generic stock-photo scenes, busy full-frame landscapes, complex cities, crowded desks, many characters, floating islands, rocky islands, grass, soil, cliffs, plants, terrain chunks, natural landscape bases, matte-gray platforms, plinths, oversized object clusters, dramatic perspective, strong shadows, saturated color, poster-like contrast, a cover/hero image, a plain mascot portrait, or arbitrary character redesign between images.

When using the default 小饭团 preset, also avoid: 3D 小饭团, realistic rice sculpture, side-profile 小饭团, redesigned 小饭团 body, long arms, human hands, fingers, circular hands, mittens, filled oval feet, shoes, toes, long legs, stick legs, crawling pose, kneeling pose, clothing, accessories, hair, hats, or realistic limbs.

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
- background color
- scene prompt notes
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
- 背景色：...
- 场景提示：使用文字规则描述注释式构图，不加载额外场景图片
- 可选文字：...
- Alt text：...
- 提示词摘要：...
```

## Quality Check

Before final response, verify:

- All planned images have matching files in `images/`.
- `guide.md` references the exact generated filenames.
- Character, character reference path, and background color are recorded in the plan and `guide.md`.
- No image relies on large visible text to explain itself.
- Each image prompt uses the resolved exact background color.
- Each image reads as a quiet inline article illustration, not a cover, poster, hero image, or attention-grabbing decorative image.
- Each image uses text-only annotated-node/storyboard scene rules.
- Each image avoids matte-gray platforms/plinths, rocky floating islands, grass islands, terrain chunks, or natural landscape bases.
- Each image leaves at least 55% calm negative space and avoids dense full-frame scenery.
- Each image uses muted colors, low contrast, and very soft shadows so the article remains the visual priority.
- Each image was generated with the selected character reference loaded, attached, or otherwise visible whenever the available image tool supports image references.
- No scene image reference was loaded or attached; scene style came from the prompt text.
- Each image keeps the protagonist's identity consistent with the selected reference.
- If using the default 小饭团 preset, each image keeps the same body shape, simple face, lower-front nori patch, short black line hands/arms, two tiny black line feet, and low detail level.
- Each image has a specific placement reason.
- Each image states what the protagonist is doing.
- The final answer lists the image files and the guide path.
