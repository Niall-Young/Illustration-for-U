---
name: fantuan-illustration-journey
description: Create quiet article and material illustrations in the 小饭团的奇妙之旅 style. Use when Codex needs to read an article, decide where images or inline illustrations should be placed, plan each image brief, generate 16:9 image_gen illustrations featuring a fixed 2D 小饭团 character on small 3D isometric floating-island vignettes over a shallow light gray background, and produce an images/ folder plus a Markdown placement guide.
---

# 小饭团的奇妙之旅

## Overview

Use this skill to turn an article, document, PRD, content draft, campaign material, or pasted text into a complete illustration package: planned insertion points, generated images, and a Markdown guide explaining where to place each image.

Always read `references/fantuan-style.md` before writing image prompts or final placement guidance.

Default visual direction: this skill creates quiet supporting illustrations for articles, not cover art, posters, or full-scene key visuals. The image should have low visual weight: a shallow light gray background, one compact 3D floating-island vignette, generous negative space, and one clear article idea per image. 小饭团 must stay as a flat 2D illustrated character placed inside that 3D scene.

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
   - style split: what is 3D in the scene and how 小饭团 remains 2D
   - visual density: the one main idea, 3-5 supporting props at most, and intended negative space
   - key visual elements: floating island shape, objects, spatial layout, sparse doodle accents
   - optional handwritten text: short, sparse note-like text only when it improves comprehension
   - alt text
4. Generate each image with `image_gen`:
   - default aspect ratio: `16:9`
   - filename pattern: `fantuan-illustration-01.png`, `fantuan-illustration-02.png`, incrementing from `01`
   - output directory: `images/`
5. Write `guide.md` after all images are ready.

## Image Prompt Requirements

Every image prompt must include:

- 16:9 article-illustration composition with a shallow light gray background.
- A compact realistic 3D isometric floating island or tiny diorama, not a full-frame environment.
- The island should occupy about 35-50% of the canvas; the rest should remain calm negative space.
- One main visual idea, with 3-5 supporting props at most.
- 小饭团 as the fixed flat 2D illustrated character described in `references/fantuan-style.md`; do not render 小饭团 as a 3D object.
- A clear style split: scene, island, props, lighting, and shadows can be 3D; 小饭团 must be flat 2D line-and-fill illustration with minimal or no 3D shading.
- Hand-drawn doodle lines and light annotation marks used sparsely around supporting elements.
- Sparse handwritten note text only when useful; avoid large blocks of visible text.
- A clear action for 小饭团.
- The reason the visual supports its article placement.

Avoid prompt wording that asks for dense typography, long labels, UI screenshots, generic stock-photo scenes, busy full-frame landscapes, complex cities, crowded desks, many characters, strong poster-like contrast, a 3D 小饭团, or a plain mascot on an empty background.

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
- 可选文字：...
- Alt text：...
- 提示词摘要：...
```

## Quality Check

Before final response, verify:

- All planned images have matching files in `images/`.
- `guide.md` references the exact generated filenames.
- No image relies on large visible text to explain itself.
- Each image uses a shallow light gray background and compact floating-island composition.
- Each image leaves generous negative space and avoids dense full-frame scenery.
- Each image keeps the scene and props 3D while keeping 小饭团 as a flat 2D illustrated character.
- Each image has a specific placement reason.
- Each image states what 小饭团 is doing.
- 小饭团 keeps the fixed character design, especially the same short rounded line-arm style.
- The final answer lists the image files and the guide path.
