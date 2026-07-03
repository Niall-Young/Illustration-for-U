# Illustration for U

<p align="right">
  <a href="#english">English</a> | <a href="#中文">中文</a>
</p>

## English

Illustration for U is a configurable Codex skill for turning articles, Markdown, PRDs, campaign copy, or pasted text into a small package of inline illustrations.

It reads the source text, chooses useful insertion points, plans each illustration, keeps a consistent character identity, applies a stable background color, generates images, and writes a `guide.md` that explains where each image should be placed.

The bundled default character is 小饭团, but the skill is designed for users to bring their own article-illustration character.

### What It Does

- Creates quiet `16:9` body illustrations for articles, not covers or posters.
- Supports a default preset character via `assets/character-reference.png`.
- Supports user-provided character reference images.
- Supports text-defined custom characters by first generating a stable reference image.
- Supports custom background colors, with `#F4F4F2` as the default.
- Produces an `images/` folder and a `guide.md` placement guide.
- Keeps the article as the visual priority: low contrast, low saturation, soft shadows, and generous whitespace.

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
3. Bundled default `assets/character-reference.png`, currently 小饭团.

For custom characters, the skill should preserve the reference character's silhouette, face, signature details, colors, line style, rendering mode, and detail density across the whole image set.

For the bundled 小饭团 preset, the stricter lock rules preserve the rounded triangular rice-ball body, dot eyes, lower-front nori patch, short black line hands, and tiny black line feet.

### Replace the Default Character Permanently

If you already have your own character image and want it to replace the bundled 小饭团 preset for every future use, replace this file:

```text
illustration-for-u/assets/character-reference.png
```

Keep the same filename and path so the skill can keep using the default reference without any other setup:

```bash
cp /path/to/your-character.png illustration-for-u/assets/character-reference.png
```

Recommended character reference:

- Use a clean PNG image.
- Prefer a square canvas or a clear full-body mascot view.
- Keep the character simple enough to remain consistent in small article illustrations.
- Avoid busy backgrounds, multiple poses, multiple characters, or heavy scene elements in the reference image.

If you are publishing your own preset, also update the text that says the bundled preset is 小饭团:

```bash
rg "小饭团|rice-ball|nori" illustration-for-u README.md
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
rg "fantuan-illustration-journey|fantuan-character-reference|fantuan-style|小饭团的奇妙之旅"
```

Keep the skill itself small:

- Put routing and trigger language in `SKILL.md` frontmatter.
- Put detailed visual rules in `references/illustration-style.md`.
- Keep `agents/openai.yaml` aligned with the current skill name and purpose.
- Treat 小饭团 as a bundled preset, not as the only supported character.
- Do not hard-code one background color as the only valid style.

### License

Add a license before publishing if this repository is intended for public reuse.

---

## 中文

Illustration for U 是一个可配置的 Codex skill，用于把文章、Markdown、PRD、活动文案或粘贴文本转换成一组正文配图。

它会先阅读原文，再选择适合插图的位置，规划每张图，保持角色形象一致，应用稳定背景色，生成图片，并输出 `guide.md` 说明每张图应该放在哪里。

内置默认角色是小饭团，但这个 skill 的目标不是绑定小饭团，而是让用户可以使用自己的配文插画形象。

### 功能

- 生成适合正文使用的安静 `16:9` 插图，不做封面图或海报图。
- 通过 `assets/character-reference.png` 提供默认预设角色。
- 支持用户上传自己的角色参考图。
- 支持用文字描述自定义角色，并先生成稳定角色参考图。
- 支持自定义背景色，默认背景色为 `#F4F4F2`。
- 输出 `images/` 图片目录和 `guide.md` 放置说明。
- 保持低对比、低饱和、柔和阴影和足够留白，让文章内容仍然是视觉重点。

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
给这篇文章配图，用默认小饭团，背景色 #F4F4F2
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
3. 内置默认 `assets/character-reference.png`，当前是小饭团。

使用自定义角色时，skill 应该在整组图片里保持参考图中的轮廓、脸部特征、标志性细节、颜色、线条风格、渲染方式和细节密度。

使用内置小饭团预设时，会应用更严格的锁定规则：保持圆润三角饭团身体、点状眼睛、下方海苔块、短小黑线手和两个 tiny black line feet。

### 永久替换默认角色

如果你已经做好了自己的角色形象，并希望它在以后每次使用时都替代内置小饭团预设，直接替换这个文件：

```text
illustration-for-u/assets/character-reference.png
```

保持同样的文件名和路径，这样 skill 不需要额外配置就会继续读取默认角色参考图：

```bash
cp /path/to/your-character.png illustration-for-u/assets/character-reference.png
```

推荐的角色参考图：

- 使用干净的 PNG 图片。
- 优先使用方形画布，或者清楚的全身 mascot 视图。
- 角色要足够简洁，方便在正文小插图里保持一致。
- 不建议在参考图里放复杂背景、多套姿势、多个角色或完整场景。

如果你准备发布自己的预设版本，还需要把文档和 skill 说明里“小饭团是默认预设”的文字一起改掉：

```bash
rg "小饭团|rice-ball|nori" illustration-for-u README.md
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
rg "fantuan-illustration-journey|fantuan-character-reference|fantuan-style|小饭团的奇妙之旅"
```

保持 skill 本身简洁：

- 把路由和触发语言放在 `SKILL.md` frontmatter。
- 把详细视觉规则放在 `references/illustration-style.md`。
- 保持 `agents/openai.yaml` 与当前 skill 名称和用途一致。
- 把小饭团作为内置 preset，而不是唯一支持角色。
- 不要把某一个背景色硬编码成唯一可用风格。

### License

如果这个仓库要公开复用，请在发布前补充 license。
