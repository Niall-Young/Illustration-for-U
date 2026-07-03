# 小饭团的奇妙之旅 / Fantuan Illustration Journey

这是一个 Codex skill，用于把文章、Markdown、PRD、活动物料或粘贴文本转换成一组“小饭团”正文配图。它不是通用生图提示词包，而是一个完整流程：读原文、选择插图位置、规划每张图、使用固定小饭团参考图生成图片，并输出 `guide.md` 放置说明。

## Skill 目录

```text
fantuan-illustration-journey/
  SKILL.md
  agents/openai.yaml
  assets/
    fantuan-character-reference.png
  references/
    fantuan-style.md
```

- `SKILL.md`：Codex 实际读取的技能入口。frontmatter `description` 是最重要的触发表面。
- `agents/openai.yaml`：Codex UI 里的展示名、短描述、默认提示和隐式触发策略。
- `assets/fantuan-character-reference.png`：固定小饭团身份参考图，生图前必须加载或附加。
- `references/fantuan-style.md`：完整视觉风格、角色锁定和提示词模板。

## 适用触发词

这个 skill 应该在用户要求“给文章配图”时优先于通用 image generation 使用。典型触发包括：

- `给文章配图`
- `给这篇文章做插图/配图`
- `按文章结构生成一组图`
- `为正文插图`
- `create article illustrations`
- `make images for an article`
- 把粘贴文本、Markdown、PRD 或活动物料转成正文插图

如果这些表达没有触发 skill，优先检查 `SKILL.md` frontmatter 的 `description`，因为正文内容只有在 skill 已经触发后才会被加载。

## 必要能力

完整使用这个 skill 需要 Image Gen 能力。

- Codex 环境需要可用的 Image Gen skill/tool，例如 `$imagegen` 或 `image_gen`。
- 没有 Image Gen 时，只能完成文章分析、插图规划和 `guide.md`，不能实际生成图片。
- 不要在没有生图能力时假装图片已经生成。
- 如果生图工具无法读取本地参考图，应先说明稳定角色需要 `assets/fantuan-character-reference.png`；只有在用户接受角色漂移风险时，才继续文本-only 方案。

## 默认输出

```text
images/
  fantuan-illustration-01.png
  fantuan-illustration-02.png
guide.md
```

`guide.md` 需要逐张说明图片路径、建议插入位置、图片用途、场景/故事、小饭团动作、参考图使用说明、场景提示词说明、可选文字、alt text 和提示词摘要。

## 视觉规则

默认比例为 `16:9`，背景固定为浅灰色 `#F4F4F2`。

画面语言是白底注释式故事板，而不是封面图、海报、复杂场景或浮岛插画。根据文章片段选择：

- `single-node focus`：一个概念或一个焦点节点。
- `two-node contrast`：两个对比节点。
- `multi-node journey`：3-5 个流程、时间线或因果节点。

可使用小物件、纸条、胶带、彩色圆点、红色下划线、少量手写批注，以及必要时的手绘连接线。连接线不是每张图都必须有；只有流程、时间线、对比或因果关系需要时才使用。

小饭团必须保持固定身份：

- 使用 `assets/fantuan-character-reference.png` 作为身份参考图。
- 小饭团保持平面 2D 插画角色；周围道具可以是轻微 cutout-like 或 soft 3D。
- 只能改变动作、姿态和周围道具，不能重新设计角色。
- 保持同一个圆润三角饭团身体、点状眼睛、下方海苔块、短小黑线手和两个 tiny black line feet。
- 不要生成长手臂、手指、手套、鞋、椭圆脚、长腿、跪姿、爬姿、3D 饭团、服装或配饰。

整体要像文章正文里的轻量插图：低视觉重量、低饱和、低对比、柔和阴影，并保留至少 55% 安静留白。

## 使用流程

1. 先读完整原文，不要直接生图。
2. 找出适合放图的位置：章节开头、关键概念转换、案例、总结或情绪节点。
3. 先写插图计划，再调用 Image Gen。每张图至少规划插入锚点、图片用途、场景结构、小饭团动作、参考图使用方式、可选手写文字和 alt text。
4. 生图时加载或附加 `assets/fantuan-character-reference.png`，并在提示词里明确它是小饭团身份参考图。
5. 使用文字提示描述场景规则，不加载额外场景参考图。
6. 图片按 `fantuan-illustration-01.png`、`fantuan-illustration-02.png` 递增命名，放入 `images/`。
7. 所有图片完成后再写 `guide.md`。
8. 最后检查图片文件和 `guide.md` 引用是否一一对应。

## 安装和同步

Codex 自动发现的技能目录通常是：

```text
~/.codex/skills/fantuan-illustration-journey
```

如果只改了本仓库副本，当前线程或新线程不一定会使用到这些改动。同步到已安装 skill：

```bash
mkdir -p "$HOME/.codex/skills/fantuan-illustration-journey"
rsync -a fantuan-illustration-journey/ "$HOME/.codex/skills/fantuan-illustration-journey/"
```

同步后可检查关键文件是否一致：

```bash
cmp -s fantuan-illustration-journey/SKILL.md "$HOME/.codex/skills/fantuan-illustration-journey/SKILL.md"
cmp -s fantuan-illustration-journey/agents/openai.yaml "$HOME/.codex/skills/fantuan-illustration-journey/agents/openai.yaml"
```

如果已安装目录是 symlink，可以直接改源目录；如果是普通目录，需要同步。

## 验证

更新 `SKILL.md` 或 `agents/openai.yaml` 后，运行基础校验：

```bash
python3 "$HOME/.codex/skills/.system/skill-creator/scripts/quick_validate.py" fantuan-illustration-journey
```

如果出现 `Invalid YAML in frontmatter: mapping values are not allowed here`，通常是 `description` 里有中英文标点、冒号或复杂短语但没有整体加引号。把 `description` 写成 quoted YAML string 后再验证。

## 维护原则

- 触发词和使用场景要放在 `SKILL.md` frontmatter `description` 里，不要只写在正文。
- UI 可见的短描述和默认提示要同步更新 `agents/openai.yaml`。
- 长风格规则优先放在 `references/fantuan-style.md`，避免 `SKILL.md` 过长。
- 固定角色规则要围绕参考图和角色锁定，不要退回纯文字描述角色。
- 如果更新参考图，先目视检查它是否仍然固定了小饭团的身体比例、短小黑线手和两个 tiny black line feet。

## English Quick Reference

Fantuan Illustration Journey is a Codex skill for turning articles, Markdown, PRDs, campaign copy, or pasted text into quiet inline illustration packages. It reads the source, chooses placement anchors, plans each image, uses `assets/fantuan-character-reference.png` as the locked mascot identity reference, generates `16:9` images on exact `#F4F4F2` backgrounds, and writes `guide.md`.

Use it before generic image generation for requests like `create article illustrations`, `make images for an article`, or Chinese prompts such as `给文章配图`.

End-to-end generation requires Image Gen. Without it, the skill should only produce analysis, an illustration plan, and `guide.md`; it must not claim image files were generated.
