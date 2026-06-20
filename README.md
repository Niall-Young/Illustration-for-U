# 小饭团的奇妙之旅 / Fantuan Illustration Journey

## 中文

这是一个用于给文章和物料配图的 Codex skill。它会先通读文章，找出适合放置配图或插图的位置，再为每张图规划场景、小故事、小饭团动作、少量可选文字和 alt text，最后生成图片并输出 `guide.md` 放置说明。

### 必要前提

必须有 Image Gen 生图能力才能完整使用这个 skill。

- Codex 环境需要可用的 Image Gen skill/tool，例如 `$imagegen` 或 `image_gen`。
- 如果没有 Image Gen，这个 skill 只能完成文章分析、配图规划和 `guide.md`，不能实际生成图片。
- 不要在没有生图能力时假装图片已经生成；应先启用或安装 Image Gen 能力。

### 默认输出

```text
images/
  fantuan-illustration-01.png
  fantuan-illustration-02.png
guide.md
```

默认图片比例为 `16:9`。图片风格为浅灰色背景上的小型 3D 等轴测浮岛 + 固定形象的平面 2D 小饭团插画角色 + 少量手绘涂鸦线条和必要时的短手写批注。它应该像文章正文里的轻量插画，而不是抢占视觉重心的封面图或复杂大场景。

## English

This is a Codex skill for creating article and content illustrations. It reads the full source material, identifies the best insertion points, plans each image scene, story moment, Fantuan character action, sparse optional text, and alt text, then generates images and writes a `guide.md` placement guide.

### Required Dependency

This skill requires Image Gen capability to run end to end.

- The Codex environment must have an Image Gen skill/tool available, such as `$imagegen` or `image_gen`.
- Without Image Gen, this skill can still analyze the article, plan illustrations, and write `guide.md`, but it cannot generate actual image files.
- Do not claim images were generated when Image Gen is unavailable; enable or install Image Gen first.

### Default Output

```text
images/
  fantuan-illustration-01.png
  fantuan-illustration-02.png
guide.md
```

The default image aspect ratio is `16:9`. The visual style combines a shallow light gray background, a small 3D isometric floating-island vignette, a fixed flat 2D illustrated Fantuan character, sparse hand-drawn doodle lines, and short handwritten note text when useful. It should read as a lightweight in-article illustration, not a cover image or complex full-scene visual.
