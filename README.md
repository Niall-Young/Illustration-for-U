# Illustration for U

<p align="right">
  <a href="#english">English</a> | <a href="#中文">中文</a>
</p>

## English

Illustration for U is a configurable Codex skill for turning articles, Markdown, PRDs, campaign copy, or pasted text into a small package of inline illustrations.

It reads the source text, chooses useful insertion points, plans each illustration, keeps a consistent character identity, applies a stable background color, generates images, and writes a `guide.md` that explains where each image should be placed.

The bundled default character is 粉色海星, but the skill is designed for users to bring their own article-illustration character.

### What It Does

- Creates quiet `16:9` body illustrations for articles, not covers or posters.
- Supports a default preset character via `assets/character-reference.png`.
- Supports user-provided character reference images.
- Supports text-defined custom characters by first generating a stable reference image.
- Encodes a per-character anatomy/structure budget in generation prompts instead of assuming every character has two hands and two feet.
- Supports custom background colors, with `#F4F4F2` as the default.
- Produces an `images/` folder and a `guide.md` placement guide.
- Keeps the article as the visual priority: low contrast, low saturation, soft shadows, and generous whitespace.
- Generates each final scene as one integrated `image_gen` output and rejects local cutout/compositing artifacts.

### Repository Structure

```text
illustration-for-u/
  SKILL.md
  agents/
    openai.yaml
  assets/
    character-reference.png
  references/
    illustration-style.md
```

- `SKILL.md` is the skill entry point. Its frontmatter `description` is the main trigger surface.
- `agents/openai.yaml` contains Codex UI metadata and the default invocation prompt.
- `assets/character-reference.png` is the bundled default character reference. Replace it if you want to publish a different default preset.
- `references/illustration-style.md` contains the detailed visual system, character-lock rules, background-color rules, and prompt pattern.

### Install

Copy or symlink the `illustration-for-u/` folder into your Codex skills directory.

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R illustration-for-u "${CODEX_HOME:-$HOME/.codex}/skills/illustration-for-u"
```

Or, if you prefer to keep editing this repository directly:

```bash
ln -s "$(pwd)/illustration-for-u" "${CODEX_HOME:-$HOME/.codex}/skills/illustration-for-u"
```

Restart or reload Codex if the skill list does not update immediately.

### Usage

Invoke the skill explicitly:

```text
Use $illustration-for-u to create illustrations for this article.
```

Typical requests:

```text
Use $illustration-for-u to make inline illustrations for this Markdown post.
Use the attached character image as the protagonist and use a pale blue background.
```

```text
Give this PRD a set of body illustrations. The character is a white round robot wearing headphones. Use #F7F3EA as the background color.
```

End-to-end image generation requires an available image generation tool. Without image generation, the skill should only produce the illustration plan and `guide.md`; it should not claim image files were created.

### Custom Character

Illustration for U resolves the character in this order:

1. User-provided character reference image.
2. User-provided text character description, converted into a task-level `images/character-reference.png`.
3. Bundled default `assets/character-reference.png`, currently 粉色海星.

For custom characters, the skill should preserve the reference character's silhouette, face, signature details, colors, line style, rendering mode, and detail density across the whole image set.

It should also preserve the character's own anatomy/structure budget in the generation prompt. A custom character may have no limbs, wheels instead of feet, wings, a tail, tentacles, or other non-human structure. The skill should describe the visible/intended body parts and absent parts before generation so the prompt does not add, remove, duplicate, or fuse body parts.

For the bundled 粉色海星 preset, the stricter lock rules preserve the five-point rounded pink starfish body, glossy dark eyes, small smile, blush cheeks, pale raised dot details, darker pink outline, and the absence of separate hands or feet.

### Integrated Output Quality

The skill must not build final illustrations by cropping the character reference and pasting it into a separate scene. Use the character reference only as identity/anatomy input for `image_gen`, then generate the whole 16:9 article illustration as one integrated image.

Do not use PIL, canvas, SVG, CSS, alpha masks, background removal, thresholding, or local scripts to composite the protagonist separately from the scene. Local image operations are only for whole-canvas tasks after approval, such as copying, renaming, metadata changes, or resizing/cropping the entire final image.

Before delivery, reject any output with a visible square/rectangular patch around the character, gray or white reference-canvas remnant, hard mask edge, background-removal halo, mismatched drop-shadow box, copied square portrait, contact sheet, or rough candidate artifact.

### Replace the Default Character Permanently

If you already have your own character image and want it to replace the bundled 粉色海星 preset for every future use, replace this file:

```text
illustration-for-u/assets/character-reference.png
```

Keep the same filename and path so the skill can keep using the default reference without any other setup:

```bash
cp /path/to/your-character.png illustration-for-u/assets/character-reference.png
```

Recommended character reference:

- Use a clean PNG image.
- Prefer a square canvas, clear full-body mascot view, or compact model sheet that shows the character's structure.
- Keep the character simple enough to remain consistent in small article illustrations.
- Avoid busy backgrounds, dense pose sheets, multiple unrelated characters, or heavy scene elements in the reference image.
- If using a model sheet, make it clear that it represents one canonical character. The final article image should not copy the sheet layout or show every pose unless the user asks.

If you are publishing your own preset, also update the text that says the bundled preset is the current character:

```bash
rg "粉色海星|pink starfish|starfish" illustration-for-u README.md
```

At minimum, review:

- `illustration-for-u/SKILL.md`
- `illustration-for-u/references/illustration-style.md`
- `illustration-for-u/agents/openai.yaml`
- `README.md`

### Custom Background

The default background color is:

```text
#F4F4F2
```

If the user specifies a color, that color takes priority. The same resolved background color should be written into the plan, every image prompt, and `guide.md`, and should remain consistent across the whole image package unless the user asks for variation.

To permanently change the global default background color, replace `#F4F4F2` everywhere the skill defines or documents the default. For example, to make `#F7F3EA` the new default:

```bash
perl -pi -e 's/#F4F4F2/#F7F3EA/g' \
  README.md \
  illustration-for-u/SKILL.md \
  illustration-for-u/references/illustration-style.md \
  illustration-for-u/agents/openai.yaml
```

Then confirm there are no old default-color references left:

```bash
rg "#F4F4F2" README.md illustration-for-u
```

If the search returns nothing, the global default color has been replaced. Users can still override the background color per request.

### Output

Default output:

```text
images/
  illustration-for-u-01.png
  illustration-for-u-02.png
guide.md
```

If the user defines a character only through text, the skill should first create:

```text
images/
  character-reference.png
```

`guide.md` should include one section per image with the file path, insertion anchor, image purpose, scene description, character action, reference-image usage, background color, optional handwritten text, alt text, and prompt summary.

### Development

Validate the skill after editing `SKILL.md` or `agents/openai.yaml`:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" illustration-for-u
```

Also check for stale names when renaming or repackaging:

```bash
rg "OLD_SKILL_NAME|OLD_CHARACTER_NAME|OLD_REFERENCE_FILE" README.md illustration-for-u
```

Keep the skill itself small:

- Put routing and trigger language in `SKILL.md` frontmatter.
- Put detailed visual rules in `references/illustration-style.md`.
- Keep `agents/openai.yaml` aligned with the current skill name and purpose.
- Treat the default character as a bundled preset, not as the only supported character.
- Do not hard-code one background color as the only valid style.

### License

Add a license before publishing if this repository is intended for public reuse.

---

## 中文

Illustration for U 是一个可配置的 Codex skill，用于把文章、Markdown、PRD、活动文案或粘贴文本转换成一组正文配图。

它会先阅读原文，再选择适合插图的位置，规划每张图，保持角色形象一致，应用稳定背景色，生成图片，并输出 `guide.md` 说明每张图应该放在哪里。

内置默认角色是粉色海星，但这个 skill 的目标不是绑定某一个角色，而是让用户可以使用自己的配文插画形象。

### 功能

- 生成适合正文使用的安静 `16:9` 插图，不做封面图或海报图。
- 通过 `assets/character-reference.png` 提供默认预设角色。
- 支持用户上传自己的角色参考图。
- 支持用文字描述自定义角色，并先生成稳定角色参考图。
- 会把角色自己的解剖/结构预算写进生成提示词，而不是默认每个角色都有两只手两只脚。
- 支持自定义背景色，默认背景色为 `#F4F4F2`。
- 输出 `images/` 图片目录和 `guide.md` 放置说明。
- 保持低对比、低饱和、柔和阴影和足够留白，让文章内容仍然是视觉重点。
- 每张最终图都必须是 `image_gen` 直接生成的完整场景，并拒绝本地抠图/拼贴造成的瑕疵。

### 项目结构

```text
illustration-for-u/
  SKILL.md
  agents/
    openai.yaml
  assets/
    character-reference.png
  references/
    illustration-style.md
```

- `SKILL.md` 是 skill 入口文件，frontmatter 里的 `description` 是最重要的触发表面。
- `agents/openai.yaml` 是 Codex UI 展示信息和默认调用提示。
- `assets/character-reference.png` 是默认角色参考图。发布自己的预设版本时，可以替换它。
- `references/illustration-style.md` 包含详细视觉系统、角色锁定规则、背景色规则和提示词模板。

### 安装

把 `illustration-for-u/` 文件夹复制或软链接到你的 Codex skills 目录。

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R illustration-for-u "${CODEX_HOME:-$HOME/.codex}/skills/illustration-for-u"
```

如果你希望直接在这个仓库里持续编辑：

```bash
ln -s "$(pwd)/illustration-for-u" "${CODEX_HOME:-$HOME/.codex}/skills/illustration-for-u"
```

如果 Codex 没有立刻显示新 skill，重启或重新加载 Codex。

### 使用

显式调用这个 skill：

```text
Use $illustration-for-u to create illustrations for this article.
```

常见请求：

```text
给这篇文章配图，用默认粉色海星，背景色 #F4F4F2
```

```text
用 $illustration-for-u 给这篇 Markdown 文章做正文插图。
使用我上传的角色图作为主角，背景色用浅蓝色。
```

```text
给这个 PRD 做一组正文插画。角色是一只戴耳机的白色圆形机器人，背景色用 #F7F3EA。
```

完整生成图片需要可用的图像生成工具。如果没有图像生成能力，skill 只能输出插图计划和 `guide.md`，不能声称已经生成图片文件。

### 自定义角色

Illustration for U 会按以下优先级确定角色：

1. 用户提供的角色参考图。
2. 用户提供的文字角色描述，并转换为任务级 `images/character-reference.png`。
3. 内置默认 `assets/character-reference.png`，当前是粉色海星。

使用自定义角色时，skill 应该在整组图片里保持参考图中的轮廓、脸部特征、标志性细节、颜色、线条风格、渲染方式和细节密度。

同时也要在生成提示词里保持这个角色自己的结构预算。用户的角色可能没有四肢，可能是轮子、翅膀、尾巴、触手，或者只是一个无肢体图形。skill 应该在生成前描述可见/设定中的身体部件和明确不存在的部件，让提示词直接避免新增、删减、复制或融合身体部件。

使用内置粉色海星预设时，会应用更严格的锁定规则：保持五角圆润粉色海星身体、深色高光眼睛、小笑脸、腮红、浅粉凸点、深粉描边，并且不添加独立手脚。

### 成片质量规则

最终插图不能通过“裁出角色参考图，再贴到另一张场景图里”的方式制作。角色参考图只作为 `image_gen` 的身份和结构参考，最终的 16:9 正文插图必须作为一个完整场景整体生成。

不要用 PIL、canvas、SVG、CSS、alpha mask、背景移除、阈值抠图或本地脚本，把主角和场景分开合成。允许的本地图像操作仅限成片通过检查之后的整张画布操作，例如复制、重命名、改元数据，或对整张最终图统一缩放/裁切。

交付前必须拒绝这些问题：角色周围出现明显方形/矩形底、灰白参考画布残留、硬边遮罩、抠图光晕、不匹配的投影框、把方形参考头像直接复制进 16:9 场景、候选图拼版或临时对比图被当成最终图。

### 永久替换默认角色

如果你已经做好了自己的角色形象，并希望它在以后每次使用时都替代内置粉色海星预设，直接替换这个文件：

```text
illustration-for-u/assets/character-reference.png
```

保持同样的文件名和路径，这样 skill 不需要额外配置就会继续读取默认角色参考图：

```bash
cp /path/to/your-character.png illustration-for-u/assets/character-reference.png
```

推荐的角色参考图：

- 使用干净的 PNG 图片。
- 优先使用方形画布、清楚的全身 mascot 视图，或者能展示角色结构的简洁设定图/model sheet。
- 角色要足够简洁，方便在正文小插图里保持一致。
- 不建议在参考图里放复杂背景、密集姿势表、多个无关角色或完整场景。
- 如果使用设定图，要让它明确表示同一个标准角色；正文插图不应该复制设定图排版，也不应该默认把每个姿势都画进最终图片。

如果你准备发布自己的预设版本，还需要把文档和 skill 说明里“当前默认预设”的文字一起改掉：

```bash
rg "粉色海星|pink starfish|starfish" illustration-for-u README.md
```

至少检查这些文件：

- `illustration-for-u/SKILL.md`
- `illustration-for-u/references/illustration-style.md`
- `illustration-for-u/agents/openai.yaml`
- `README.md`

### 自定义背景

默认背景色是：

```text
#F4F4F2
```

如果用户指定了背景色，以用户指定颜色为准。解析后的背景色应该写进插图计划、每张图的提示词和 `guide.md`，并在整组图片中保持一致，除非用户明确要求每张图变化。

如果想一劳永逸地更改全局默认背景色，把 skill 中定义或说明默认背景色的 `#F4F4F2` 全部替换掉即可。例如要把默认背景色改成 `#F7F3EA`：

```bash
perl -pi -e 's/#F4F4F2/#F7F3EA/g' \
  README.md \
  illustration-for-u/SKILL.md \
  illustration-for-u/references/illustration-style.md \
  illustration-for-u/agents/openai.yaml
```

然后确认旧默认色没有残留：

```bash
rg "#F4F4F2" README.md illustration-for-u
```

如果搜索没有结果，就说明全局默认背景色已经替换完成。用户在单次请求中仍然可以临时指定其他背景色。

### 输出

默认输出：

```text
images/
  illustration-for-u-01.png
  illustration-for-u-02.png
guide.md
```

如果用户只用文字定义角色，skill 应该先创建：

```text
images/
  character-reference.png
```

`guide.md` 应该为每张图写明图片路径、插入位置、图片用途、场景描述、角色动作、角色参考图使用方式、背景色、可选手写文字、alt text 和提示词摘要。

### 开发

修改 `SKILL.md` 或 `agents/openai.yaml` 后，运行校验：

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" illustration-for-u
```

重命名或重新打包时，检查旧名称残留：

```bash
rg "OLD_SKILL_NAME|OLD_CHARACTER_NAME|OLD_REFERENCE_FILE" README.md illustration-for-u
```

保持 skill 本身简洁：

- 把路由和触发语言放在 `SKILL.md` frontmatter。
- 把详细视觉规则放在 `references/illustration-style.md`。
- 保持 `agents/openai.yaml` 与当前 skill 名称和用途一致。
- 把默认角色作为内置 preset，而不是唯一支持角色。
- 不要把某一个背景色硬编码成唯一可用风格。

### License

如果这个仓库要公开复用，请在发布前补充 license。
