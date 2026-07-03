# Repository Guidelines

## Project Scope

- This repository maintains the `illustration-for-u` Codex skill.
- Treat `illustration-for-u/` as the active skill package; repository-level files such as `README.md` document how to install, use, and maintain it.
- Do not treat this as a generic web, Node, or image-generation app. There may be no `package.json`.

## Skill Contract

- `illustration-for-u/SKILL.md` is the skill entry point.
- The YAML frontmatter `description` is the main trigger surface. Keep article-illustration trigger phrases in that description, especially Chinese requests such as `给文章配图`, `给这篇文章做插图/配图`, `按文章结构生成一组图`, and English requests such as `create article illustrations` or `make images for an article`.
- `image_gen` is only the downstream image generation tool. It must not replace the skill workflow: read the source, choose placement anchors, resolve character/background configuration, plan prompts, generate files, and write `guide.md`.
- `illustration-for-u/references/illustration-style.md` holds detailed visual rules. Keep long style, character-lock, background-color, and prompt-pattern rules there instead of bloating the skill entrypoint.
- `illustration-for-u/agents/openai.yaml` must stay aligned with the skill name, short description, and default invocation prompt.

## Output Contract

- The skill generates quiet `16:9` inline article illustrations, not cover art, poster art, hero images, generic stock scenes, or full-scene key visuals.
- Default output is:

```text
images/
  illustration-for-u-01.png
  illustration-for-u-02.png
guide.md
```

- If the user defines a custom character only through text, first create:

```text
images/
  character-reference.png
```

- `guide.md` must reference the exact generated filenames and include placement anchor, image purpose, scene/story, character action, character reference usage, character structure constraints, background color, scene prompt notes, acceptance notes, optional short handwritten text, alt text, and prompt summary.

## Character And Background Rules

- Resolve the character before planning images:
  - user-provided reference image first,
  - text-defined character converted into `images/character-reference.png` second,
  - bundled `illustration-for-u/assets/character-reference.png` preset last.
- The bundled default preset is currently `粉色海星`; do not hard-code that anatomy onto custom characters.
- Derive a compact character structure budget from the selected reference or user description before writing prompts. Preserve the character's own silhouette, appendage count/type, face, signature details, colors, line style, rendering mode, and detail density.
- Do not assume every custom character has two hands and two feet. Record absent parts as absent and avoid prompt actions that require inventing new anatomy.
- Use the user's requested background color when provided. Otherwise use the default `#F4F4F2`.
- Keep the resolved background color consistent in the plan, every image prompt, and `guide.md` unless the user explicitly asks for variation.

## Image Quality Rules

- Final article images must be whole-scene `image_gen` generations.
- Do not crop, segment, threshold, alpha-mask, background-remove, or paste the protagonist into another generated scene with PIL, canvas, SVG, CSS, or local image-editing scripts.
- Use the selected character reference only as identity/anatomy guidance; do not copy the square reference-canvas composition into final `16:9` images.
- Before delivery, reject outputs with visible square or rectangular patches around the protagonist, gray/white canvas remnants, hard mask edges, background-removal halos, pasted shadows, copied square portraits, contact sheets, or rough candidate artifacts.

## Editing Guidelines

- Prefer small, scoped edits that preserve the existing skill workflow and output contract.
- When changing the default character, review and update all preset mentions in:
  - `README.md`
  - `illustration-for-u/SKILL.md`
  - `illustration-for-u/references/illustration-style.md`
  - `illustration-for-u/agents/openai.yaml`
- When changing the default background color, replace it consistently across the same files and verify no old default remains.
- When renaming the skill or folder, immediately search for stale names in `README.md` and `illustration-for-u/`.
- Do not revert user changes unless explicitly requested. Keep unrelated files untouched.

## Commands

- Use `rg` for searching files and text.
- Inspect the repository before assuming a build system exists.
- Validate the skill after editing `SKILL.md` or `agents/openai.yaml`:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" illustration-for-u
```

- Useful consistency checks:

```bash
rg "粉色海星|pink starfish|starfish" README.md illustration-for-u
rg "#F4F4F2" README.md illustration-for-u
rg "OLD_SKILL_NAME|OLD_CHARACTER_NAME|OLD_REFERENCE_FILE" README.md illustration-for-u
```

## Verification

- Use the narrowest relevant command before reporting completion.
- For metadata or routing edits, run `quick_validate.py` when available.
- For documentation-only edits, at minimum inspect the changed file and use `rg` to verify important names, paths, and defaults still match the skill package.
