---
name: fantuan-illustration-journey
description: "Create article and material illustration packages in the 小饭团的奇妙之旅 style. Use whenever the user asks in Chinese or English to 给文章配图, 给这篇文章做插图/配图, 按文章结构生成一组图, 为正文插图, create article illustrations, make images for an article, or turn pasted text/Markdown/PRDs/campaign materials into inline illustrations. Trigger this before generic imagegen: read the source, choose placement anchors, plan each brief, load only assets/fantuan-character-reference.png as the fixed mascot identity reference, apply the extracted whiteboard annotated-node scene prompt rules, generate quiet 16:9 image_gen illustrations on exact fixed #F4F4F2 backgrounds by changing 小饭团's action/pose inside annotated scenes with optional story nodes, connector lines, notes, tape, colored dots, and red underlines, and produce an images/ folder plus guide.md."
---

# 小饭团的奇妙之旅

## Overview

Use this skill to turn an article, document, PRD, content draft, campaign material, or pasted text into a complete illustration package: planned insertion points, generated images, and a Markdown guide explaining where to place each image.

Always read `references/fantuan-style.md` before writing image prompts or final placement guidance. Use `assets/fantuan-character-reference.png` as the only image reference for generation. Scene style is prompt text only, not an image reference.

Use `image_gen` only as the downstream generation tool. Do not replace this skill's article reading, placement planning, prompt planning, file naming, or guide-writing workflow with a generic image generation flow.

Default visual direction: this skill creates quiet supporting illustrations for articles, not cover art, posters, decorative hero images, or full-scene key visuals. The article is the main content; illustrations must feel like small inline visual essays that support reading without competing for attention. Use the exact fixed background color `#F4F4F2`. The scene should follow a clean whiteboard annotated-node/storyboard language: one or more small visual nodes, tiny paper scraps or tape tabs, sparse colored dots, red underlines, and short handwritten annotations. Choose the structure from the article moment: a single concept can be one annotated node with no connector line; a contrast can use two separated nodes; a process, journey, or timeline can use 3-5 nodes arranged left-to-right with thin hand-drawn black connector lines or arrows. Use small cutout-like objects and props with soft shadows, but do not use matte-gray platforms, plinths, floating islands, rocky terrain, grass, soil, cliffs, plants, or scenic bases. 小饭团 must stay as the same flat 2D mascot in every image, interacting with the relevant node or path.

小饭团 character consistency is mandatory. Treat `assets/fantuan-character-reference.png` as the locked mascot sheet, not a loose inspiration image and not a character to redesign per scene.

Reference-image workflow:

- Before the first `image_gen` call, load, view, or attach `assets/fantuan-character-reference.png` so the image generation step can see the mascot reference. Use the PNG as the primary identity input; the text rules below are secondary guardrails.
- In every image prompt, explicitly say that the loaded reference image is the identity reference for 小饭团 and that only pose/action may change.
- In every image prompt, state the scene style as text: exact `#F4F4F2` background, whiteboard annotated-node composition, small object clusters, optional hand-drawn connector lines, paper/tape details, colored dots, red underlines, and sparse handwritten notes.
- Do not ask image generation to invent 小饭团 from text alone when the reference image can be supplied or made visible.
- Do not copy the square reference-canvas composition into the article illustration. Use only the mascot identity from the reference; the final illustration must still be a 16:9 article scene.
- Keep 小饭团 as one character. Do not reproduce multiple reference-sheet copies unless the user explicitly asks for multiple mascots.
- Do not make 小饭团 match the scene style by turning it into a 3D cutout, realistic object, new sticker style, or new body design. The scene can change; the mascot identity cannot.
- If the reference PNG is missing or visibly unsuitable, use Image Gen to create a new fixed square mascot reference first, save it as `assets/fantuan-character-reference.png`, inspect it, and only then generate article illustrations.
- If image generation cannot use or see the 小饭团 image reference, do not generate final images by default. Produce the illustration plan and explain that stable mascot output requires the reference image; proceed with text-only fallback only if the user explicitly accepts the drift risk.

Locked mascot rules:

- Keep the same compact rounded triangular body in every image: upright front or slight 3/4 front view, soft off-white fill, smooth black outline, flat sticker-like rendering, no side-profile body, no crawling/kneeling body, no stretched body.
- Keep the same simple face: two small dark dot eyes, optional tiny mouth only, tiny blush optional, no eyebrows, no expressive detailed face, no changed eye style.
- Keep the same lower-front nori patch: dark green/charcoal rounded rectangle centered on the lower third of the body, about one-third of body height, not a bag, clothing, shadow, or movable prop.
- Keep hands/arms as two short rounded dark charcoal line strokes attached to the body sides, like 小黑线手. Arm length should stay short, about 20-30% of body width. No long reaching arms, elbows, human hands, index fingers, separated fingers, gloves, sleeves, mittens, circles, or detailed hands.
- Keep feet as exactly two tiny dark charcoal curved line strokes tucked directly under the body, like 小黑线脚. Each foot is a short rounded-cap line, not a filled oval blob, shoe, toe shape, stick leg, long thin leg, crawling leg, kneeling leg, or foot extending far from the body.
- Keep detail level consistent across the image set: at most 2-3 subtle flat rice-grain marks, no realistic rice texture, no uneven sketch complexity, no extra accessories, clothes, hair, hats, or props attached to the body.
- Express action with nearby props, small body tilt, and short line arms; do not change mascot anatomy to fit the action.

## Workflow

1. Read the full source material before planning images.
2. Identify the best places for illustrations:
   - Prefer major section openings, important concept transitions, examples, summaries, or emotional beats.
   - Do not create an image for every paragraph.
   - Merge nearby ideas into one illustration when they serve the same reader need.
3. Create an image plan before generating anything. For each planned image, specify:
   - placement anchor: heading, paragraph summary, quote, or nearby text
   - image purpose: what the reader should understand or feel
   - scene/story: whether this is a small story moment or a single explanatory image
   - 小饭团 action: what 小饭团 is doing in the scene
   - 小饭团 reference use: confirm `assets/fantuan-character-reference.png` is used as the mascot identity reference and how only the action/pose changes
   - scene prompt use: choose and describe the whiteboard annotated-node/storyboard scene rules in text; do not use any scene image as a generation reference
   - scene structure: choose `single-node focus`, `two-node contrast`, or `multi-node journey` based on the article moment
   - style split: what objects are cutout-like/soft 3D and how 小饭团 remains flat 2D
   - visual weight: the one main idea, 1-5 small nodes as needed, at least 55% calm negative space, muted color, and soft shadow level
   - key visual elements: object node(s), optional left-to-right story path, optional connector line, paper scraps/tape tabs, colored dots, red underlines, sparse doodle accents
   - optional handwritten text: short, sparse note-like text only when it improves comprehension
   - alt text
4. Generate each image with `image_gen`:
   - load or attach `assets/fantuan-character-reference.png` as the identity reference for 小饭团
   - preserve the mascot's silhouette, face, nori patch, short black line hands/arms, two tiny black line feet, and flat 2D line-and-fill rendering from the reference
   - change only the scene-specific action/pose through small arm angle changes, a tiny body tilt, nearby props, and sparse motion marks
   - build the scene as a whiteboard annotated-node/storyboard composition, not a platform, diorama, or floating island; use connector lines only when the idea needs sequence, movement, comparison, or causality
   - default aspect ratio: `16:9`
   - filename pattern: `fantuan-illustration-01.png`, `fantuan-illustration-02.png`, incrementing from `01`
   - output directory: `images/`
5. Write `guide.md` after all images are ready.

## Image Prompt Requirements

Every image prompt must include:

- 16:9 article-illustration composition with the exact fixed background color `#F4F4F2`.
- Use `assets/fantuan-character-reference.png` as an input image / visible reference for 小饭团's identity. The reference controls the mascot's body, face, nori patch, arm style, line weight, fill colors, and flat 2D rendering.
- Describe scene composition in prompt text only: exact `#F4F4F2` canvas, small object nodes, optional thin hand-drawn black connector lines, tape/paper scraps, colored dots, red underlines, and sparse handwritten notes.
- A whiteboard annotated-node/storyboard scene with 1-5 small nodes based on the article moment. Each node should be a compact object cluster or tiny story moment, not a platform or island.
- One clear article idea, represented as either a single focal annotated node, a two-node contrast, or a short visual journey. Use cutout-like objects, small props, paper cards, and annotation marks rather than a central diorama.
- Low visual weight: at least 55% calm negative space, muted colors, low contrast, small subject scale, very soft shadows, no dramatic lighting, and no strong foreground object.
- 小饭团 as the fixed flat 2D illustrated character from the reference PNG and described in `references/fantuan-style.md`; do not render 小饭团 as a 3D object.
- 小饭团 must use the same locked mascot design across all images: same upright rounded triangular body, same dot eyes, same lower-front nori patch, same short rounded black line hands/arms, same two tiny black line feet, same simple detail level, and no anatomical redesign for different actions.
- Feet must stay as two tiny dark curved line strokes tucked directly under the body. Never use filled oval blobs, shoes, toes, stick legs, long thin legs, crawling legs, or kneeling legs.
- A clear style split: objects, paper scraps, tape, props, lighting, and shadows can be cutout-like/soft 3D; 小饭团 must be flat 2D line-and-fill illustration with minimal or no 3D shading.
- Hand-drawn black connector lines and arrows are optional. Use them only to express sequence, movement, comparison, causality, or a journey; otherwise use circles, colored dots, red underlines, tape tabs, and light annotation marks around a single node.
- Sparse handwritten note text only when useful; use short note-like labels, not paragraphs.
- A clear action for 小饭团 that changes pose/action only, not anatomy.
- The reason the visual supports its article placement.

Avoid prompt wording that asks for dense typography, long labels, UI screenshots, generic stock-photo scenes, busy full-frame landscapes, complex cities, crowded desks, many characters, floating islands, rocky islands, grass, soil, cliffs, plants, terrain chunks, natural landscape bases, matte-gray platforms, plinths, oversized object clusters, dramatic perspective, strong shadows, saturated color, poster-like contrast, a cover/hero image, a 3D 小饭团, side-profile 小饭团, redesigned 小饭团 body, long arms, human hands, fingers, circular hands, mittens, filled oval feet, shoes, toes, long legs, stick legs, crawling pose, kneeling pose, clothing, accessories, or a plain mascot on an empty background.

## Output Contract

Create this structure in the user's requested output location:

```text
images/
  fantuan-illustration-01.png
  fantuan-illustration-02.png
guide.md
```

`guide.md` must include one section per image with:

- image file path
- suggested insertion location, preferably anchored by heading, paragraph summary, or quote
- image purpose
- scene/story description
- 小饭团 action
- 小饭团参考图使用说明
- 场景提示词说明
- optional handwritten short text, or `无`
- alt text
- generation prompt summary

## Guide Template

```markdown
# 小饭团配图放置说明

## fantuan-illustration-01.png

- 图片路径：images/fantuan-illustration-01.png
- 建议位置：放在「...」标题下，... 段之前
- 图片用途：...
- 场景/故事：...
- 小饭团动作：...
- 小饭团参考：使用 assets/fantuan-character-reference.png 作为身份参考，仅改变动作/姿态
- 场景提示：使用文字规则描述 #F4F4F2 白底注释式构图，不加载额外场景图片
- 可选文字：...
- Alt text：...
- 提示词摘要：...
```

## Quality Check

Before final response, verify:

- All planned images have matching files in `images/`.
- `guide.md` references the exact generated filenames.
- No image relies on large visible text to explain itself.
- Each image prompt uses the exact fixed background color `#F4F4F2`.
- Each image reads as a quiet inline article illustration, not a cover, poster, hero image, or attention-grabbing decorative image.
- Each image uses text-only whiteboard annotated-node/storyboard scene rules: exact `#F4F4F2` background, one or more small nodes, optional hand-drawn connector lines, sparse handwritten annotations, tape/paper details, colored dots, and red underlines.
- Each image avoids matte-gray platforms/plinths, rocky floating islands, grass islands, terrain chunks, or natural landscape bases.
- Each image leaves at least 55% calm negative space and avoids dense full-frame scenery.
- Each image uses muted colors, low contrast, and very soft shadows so the article remains the visual priority.
- Each image keeps objects/props/paper/tape as cutout-like or soft 3D while keeping 小饭团 as a flat 2D illustrated character.
- Each image was generated with `assets/fantuan-character-reference.png` loaded, attached, or otherwise visible as the identity reference whenever the available image tool supports image references.
- No scene image reference was loaded or attached; scene style came from the prompt text.
- Each image keeps 小饭团's mascot anatomy consistent: same body shape, same simple face, same lower-front nori patch, same short black line hands/arms, same two tiny black line feet, and same low detail level.
- Each image has a specific placement reason.
- Each image states what 小饭团 is doing.
- 小饭团 keeps the fixed character design, especially the same short rounded line-arm style.
- The final answer lists the image files and the guide path.
