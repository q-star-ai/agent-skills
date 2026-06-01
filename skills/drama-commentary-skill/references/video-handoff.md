# Video Handoff

Use this reference when `drama-commentary-skill` consumes the output of `video-understanding-skill`.

The commentary layer should not re-interpret raw video from scratch if a structured understanding package already exists.

## Input contract

The preferred upstream input is the structured result defined in:

- `/Users/tiger/Desktop/项目文件夹/skills/video-understanding-skill/references/output-schema.md`

At minimum, the commentary layer should try to read:

- `story`
- `scenes`
- `highlights`
- `transcript.segments`
- `uncertainties`

## Consumption priority

Use the understanding package in this order:

1. `highlights`
2. `story`
3. `scenes`
4. `transcript.segments`
5. `uncertainties`

That means:

- start from what matters most for storytelling
- use transcript as support, not as the only source of truth

## How commentary should use each section

### 1. `highlights`

Use for:

- hook line selection
- reversal emphasis
- climax emphasis
- commentary-worthy clip candidates

If a highlight is tagged `hook`, `reversal`, or `climax`, treat it as high-priority material.

### 2. `story`

Use for:

- overall commentary outline
- one-paragraph story summary
- deciding what can be skipped

This should drive the main arc of the script.

### 3. `scenes`

Use for:

- local detail
- scene order validation
- emotional rhythm
- clip grouping

This is especially useful when deciding how much setup to compress.

### 4. `transcript.segments`

Use for:

- grounding specific lines
- recovering exact wording if needed
- aligning narration to time ranges

Do not let transcript dominate over story structure.

### 5. `uncertainties`

Use for:

- avoiding overclaiming
- softening or skipping weak sections
- deciding where manual review may be needed

If `story.reversal` is marked uncertain, do not build the whole hook around it.

## Recommended commentary drafting pattern

When an understanding package exists, draft in this order:

1. pick hook from `highlights`
2. take the main arc from `story`
3. use `scenes` to compress or expand beats
4. use `transcript.segments` for grounding details
5. check `uncertainties` before finalizing the narration draft

## Clip selection rule

When selecting source-video clips for the commentary draft:

- prefer `highlights` first
- then use scene boundaries for supporting clips
- only go down to transcript-level alignment when needed

This keeps the edit story-driven instead of transcript-driven.

## Minimum viable handoff

Even if the understanding result is partial, commentary can still proceed if these exist:

- `story.one_paragraph_summary`
- at least 3 useful `highlights`
- a non-empty `scenes` list or partial transcript

If fewer than 3 useful highlights exist, commentary should slow down and avoid pretending it has strong shot selection confidence.

## Sample extraction view

The commentary layer can normalize upstream output into a compact internal view like:

```json
{
  "hook_candidates": [
    {
      "highlight_id": "hl_001",
      "start_sec": 12,
      "end_sec": 18,
      "summary": "the killer appears behind him",
      "reason": "strong suspense reveal"
    }
  ],
  "story_arc": {
    "opening": "...",
    "setup": "...",
    "escalation": "...",
    "reversal": "...",
    "climax": "...",
    "ending": "..."
  },
  "supporting_scenes": [
    {
      "scene_id": "scene_003",
      "start_sec": 120,
      "end_sec": 168,
      "summary": "the first direct confrontation"
    }
  ],
  "uncertainties": [
    {
      "field": "story.ending",
      "reason": "low subtitle confidence"
    }
  ]
}
```

This normalized view is often easier for prompt construction than the full raw upstream payload.
