---
name: qstar-video-ecom
version: 1.3.2
author: qstar
emoji: "🎬"
tags:
  - video
  - ecommerce
  - ai-video
  - chinese
  - product-video
  - tiktok
  - douyin
  - xiaohongshu
  - short-video
  - marketing
  - chinese-ecommerce
  - video-generation
  - ai-marketing
description: >
  Generate AI product videos for Chinese e-commerce platforms with Chinese TTS voiceover.
  Supports Taobao, Douyin/TikTok, Xiaohongshu, Pinduoduo, JD.com, and Video Account.
  Auto-selects platform aspect ratio and duration. Upload product images for personalized
  videos when available. The workflow keeps legacy video API endpoints explicit and falls
  back to structured regeneration when a direct upload path is unavailable.
---

# 🎬 电商视频生成

Use this skill when the user wants a reviewable product-video package for a Chinese e-commerce workflow.

## Core rule

Follow this line:

`brief -> platform selection -> script -> voice -> image decision -> generate -> qc -> delivery`

Keep the workflow simple and explicit. Do not invent backend capabilities that are not exposed by the current service.

## Use cases

Use this skill for:

- product introduction videos
- e-commerce ad videos
- platform-specific product clips
- short marketing videos for Douyin / Xiaohongshu / TikTok / Taobao / Pinduoduo / JD.com / Video Account

Do not use this skill for:

- character-driven drama commentary
- long-form movie recap
- general-purpose image editing
- non-product branded motion graphics

## Required input

Prefer this input shape:

`产品名 + 面向人群 + 核心卖点`

Useful optional inputs:

- platform
- product images
- voice preference
- budget / quota state
- whether the user wants a generic video or an image-based personalized video

## Workflow

1. Build a brief.
2. Select a platform and aspect ratio.
3. Draft the script, subtitle text, title candidates, and cover line.
4. Decide whether to use user images, official images, or a fallback visual.
5. Generate the voiceover.
6. Assemble the draft video.
7. Run QC.
8. If the output becomes formal, keep Qiniu as the public anchor.

## Platform map

- `1` -> `taobao`
- `2` -> `pinduoduo`
- `3` -> `xiaohongshu`
- `4` -> `douyin`
- `5` -> `jingdong`
- `6` -> `shipinhao`

## Voice map

- `1` -> `female`
- `2` -> `male`

## Image rule

If upload-image works, prefer the personalized path.
If upload-image is not available, fall back to a structured regeneration flow using `image_url` or a generic product visual.

## Payment rule

When quota is exhausted:

1. show the available package
2. let the user choose a payment channel
3. create the order
4. send the QR code / payment instructions
5. poll until paid
6. resume from image upload or direct generation

## Operational notes

- Generation usually takes about 3 minutes.
- Keep progress messages short and explicit.
- User identity must stay in `{platform}:{sender_id}` form so cross-platform quota stays isolated.
- `upload-image` may not always exist, so the skill must tolerate a direct `image_url` flow.
- The current service keeps `/sora-api` as a legacy path name; that is an endpoint label, not a promise about the underlying model.

## References

- [Workflow notes](references/workflow.md)
- [Templates](references/templates.md)
