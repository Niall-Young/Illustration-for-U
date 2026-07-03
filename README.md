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

默认图片比例为 `16:9`。背景固定使用浅灰色 `#F4F4F2`。图片风格为白底注释式故事板：按内容选择单节点、双节点对比或多节点过程图，配合小物件、纸条/胶带、彩色圆点、红色下划线、少量手写批注和必要时的手绘连接线。小饭团是固定形象的平面 2D 插画角色，应该像文章正文里的轻量插图，而不是抢占视觉重心的封面图或复杂大场景。

### 固定角色参考图

为了避免小饭团在多次生图中出现手脚、身体比例和表情漂移，skill 内置了固定角色参考图：

```text
fantuan-illustration-journey/assets/fantuan-character-reference.png
```

这张 PNG 本身由 Image Gen 生成，是每次生图时使用的身份参考图。参考图固定了小饭团的线条小黑手和线条小黑脚。执行 skill 时应先加载/附加 PNG，再让 Image Gen 只改变小饭团的动作、姿态、周围道具和场景，不要重新从文字描述里发明角色。

### 场景提示词规则

场景不使用图片参考，只用文字提示词规则：固定 `#F4F4F2` 背景、小节点、纸条/胶带、彩色圆点、红色下划线、手写批注，以及在流程或时间线需要时才出现的手绘连接线。不要固定每张图都有连接线；单一概念可以只有一个注释节点。

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

The default image aspect ratio is `16:9`. The background must use the exact fixed light gray `#F4F4F2`. The visual style uses a text-prompted annotated storyboard scene: choose a single node, two contrast nodes, or a multi-node process based on the article moment, with small objects, paper/tape scraps, colored dots, red underlines, sparse handwritten notes, and hand-drawn connector lines only when useful. Fantuan stays as the fixed flat 2D illustrated character. The image should read as a lightweight in-article illustration, not a cover image or complex full-scene visual.

### Locked Character Reference

To reduce mascot drift across generations, the skill includes a fixed character reference:

```text
fantuan-illustration-journey/assets/fantuan-character-reference.png
```

The PNG itself was generated with Image Gen. It fixes Fantuan's tiny black line hands and tiny black line feet. Use it as the identity reference for image generation. Skill runs should load or attach the PNG first, then ask Image Gen to change only Fantuan's action, pose, nearby props, and scene instead of reinventing the character from text.

### Scene Prompt Rules

The scene does not use an image reference. Express it as prompt text only: exact `#F4F4F2` background, small nodes, paper/tape scraps, colored dots, red underlines, handwritten notes, and hand-drawn connector lines only when a process or timeline needs them. Do not force every image to have connectors; a single concept can be one annotated node.
