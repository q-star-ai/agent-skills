# Workflow

This skill supports a low-touch Chinese e-commerce product-video line.

## Goal

Produce a reviewable short-form package from minimal user input.

The standard output package is:

- brief
- platform selection
- product description
- voice choice
- script
- subtitle copy
- image decision
- generated video
- QC result

## Standard steps

### 1. Build a brief

Normalize user input into:

- product
- audience
- core value
- source images
- proof points
- CTA

### 2. Select platform

Map the request to one publishing target:

- Taobao / Tmall
- Pinduoduo
- Xiaohongshu
- Douyin / TikTok
- JD.com
- Video Account

### 3. Draft copy

Create:

- a short voiceover script
- subtitle text
- title candidates
- cover line

Default structure:

1. pain point
2. one-line definition
3. three strongest value points
4. who it is for
5. CTA

### 4. Decide on images

Preferred order:

1. user product images
2. official product page images
3. browser screenshots
4. generic fallback visual

If upload-image is unavailable, regenerate with `image_url` or a structured fallback flow.

### 5. Generate voiceover

Use the existing stable TTS path.

The default voice should be:

- clear
- neutral
- low-drama
- consistent across this line

### 6. Assemble

Prefer a fixed template over fancy editing.

Default timing:

- 0-3s hook
- 3-45s three value points
- 45-55s audience fit
- 55-60s CTA

### 7. QC

Check:

- sync
- subtitle quality
- safe crop area
- title / cover consistency
- duration

### 8. Archive

When the output becomes formal, keep Qiniu as the public anchor and avoid leaking internal-only notes into the shared package.