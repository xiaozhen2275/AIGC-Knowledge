---
name: aigc-poster-generator
description: Generate or prepare prompts for AIGC course and workshop posters from a poster design brief. Use when the user asks to create cover posters, product main images, introduction images, product long images, Image2 generations, or prompts for Jimeng, Kling, or other image models based on files such as 10_海报设计简报.md.
---

# AIGC Poster Generator

Use this skill to generate poster assets from a design brief in a controlled sequence. Do not generate all poster types at once. Always preserve one unified visual system across every image in the same project.

## Required Context

Before doing poster work, read:

1. `AGENTS.md`
2. `00_AGENT初始化总纲.md`
3. `10_海报设计简报.md`

If the user points to another poster brief, read that brief instead of `10_海报设计简报.md`.

## Workflow Gate

Follow this order exactly:

1. Understand and confirm the global design direction.
2. Generate only the 3 cover images from section `三、3 张封面图（1080x1080）`.
3. After user confirmation, generate all images from section `四、商品主图/介绍图`.
4. After product images are complete, generate section `五、产品介绍长图`.

Never skip the cover-preview gate. If the 3 covers do not meet expectations, return to step 1 and adjust the global style, palette, layout logic, and people/no-people strategy before generating again.

## Step 1: Confirm Global Style

Read the design brief for:

- design concept
- color palette
- typography and layout mood
- repeated visual elements
- poster sections and required image counts
- constraints and things to avoid

If the brief already has a design style and color palette, ask:

```text
是否按设计文档现有风格执行？
```

Also ask:

```text
是否需要包含人物海报？
```

If the user wants to adjust style, color, or references, ask for one or more of:

- poster template
- reference image or screenshot
- brand colors
- style keywords
- examples of designs they like or dislike

Global rule: any style, color, character, layout, or reference adjustment applies to the whole poster set. Do not make each image use a different style system.

## Step 2: Generate 3 Cover Images

Generate only the 3 cover images from section `三、3 张封面图（1080x1080）`.

Requirements:

- size: `1080x1080`
- keep the same color system, visual language, and layout family
- preserve each cover's own title, subtitle, information strip, action line, and composition goal
- avoid unreliable small Chinese text inside generated images when using image models; prefer clean large Chinese titles and leave detailed text for post-production if needed

After generating, stop and ask the user to confirm:

```text
这 3 张封面图的整体风格、配色、人物策略和版式方向是否通过？
```

If not approved, return to step 1. Do not continue to product images.

## Step 3: Generate Product Main/Intro Images

Only after the covers are approved, generate all images from section `四、商品主图/介绍图`.

Requirements:

- use the same approved global style
- generate the full number of images present in the brief; do not invent or omit cards
- maintain consistent title scale, card rhythm, background texture, accent colors, and icon style
- keep each image focused on its own role: path, experience, method, outcome, knowledge asset, sign-up information, or other brief-defined purpose

After generating, briefly summarize which images were produced and any text that should be overlaid manually for precision.

## Step 4: Generate Product Long Image

Before generating section `五、产品介绍长图`, confirm all variable event information:

- price
- date and time
- venue name
- full address
- QR code image or QR code content
- registration/contact method

If any information is missing, ask for it before generating. Do not hard-code old activity details from the brief unless the user explicitly confirms them.

Requirements:

- use the approved global style from the covers
- preserve the long-image screen order from the brief
- ensure QR code area remains clean and scannable
- keep action copy short enough for a mobile poster
- if using image generation, avoid relying on the model for dense Chinese text; provide exact overlay text separately when needed

## Generation Mode

### Codex With Image Generation

When Codex has an image generation tool available, directly generate images in the required stage order. Use one prompt per image or per coherent batch. Do not include later-stage images in an earlier-stage prompt.

### Other Agents With Image API

If another agent has an image generation API, output structured prompts with:

- image name
- size
- objective
- visual layout
- color palette
- required text
- negative constraints
- post-production text overlay notes

### Other Agents Without Image API

If no image API is available, output copy-ready prompts for Jimeng, Kling, or similar image models. Include:

- global style prompt
- one prompt per poster
- negative prompt
- exact text overlay list
- generation order and confirmation gate

## Quality Checks

Before presenting outputs, verify:

- the current stage matches the workflow gate
- all generated images share one visual system
- any style changes apply globally
- cover images are approved before product images
- product images are complete before the long image
- long image variable information is confirmed before generation
- the output still supports a low-pressure 2-hour workshop with visible takeaways
