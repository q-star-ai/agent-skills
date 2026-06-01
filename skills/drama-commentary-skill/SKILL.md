---
name: drama-commentary-skill
description: Use this skill when the task is to turn a user-provided, lawful movie or short-drama video into a commentary draft package with script, Chinese narration, candidate assets, and a reviewable video draft.
---

# Drama Commentary Skill

Use this skill for `剧情解说` production.

This skill is for:

- movie commentary
- short-drama recap
- plot summary videos
- first-pass commentary drafts from a source video

This skill is not for:

- downloading unauthorized films from the internet
- bypassing copyright restrictions
- using unreviewed external assets directly in final export

Read these references first:

- [style-profiles.md](references/style-profiles.md)
- [workflow.md](references/workflow.md)
- [pronunciation-draft.md](references/pronunciation-draft.md)
- [asset-integration.md](references/asset-integration.md)
- [video-handoff.md](references/video-handoff.md)

## Core rule

Follow this line:

`source video -> video understanding -> commentary script -> narration draft -> candidate assets -> user selection -> draft video`

Keep the workflow simple and consistent.

## Required input

Prefer these inputs:

- source video file or lawful upload URL
- title
- target duration
- commentary style

Useful optional inputs:

- output language
- preferred voice style
- suspense / emotional / high-energy preference
- whether image candidates are needed
- whether BGM candidates are needed

If the user gives only a title and expects automatic full-film downloading, stop and redirect to a lawful source input.

## Operating assumptions

- the source video comes from the user
- commentary is generated from that source video
- external images and BGM are fallback materials, not the main source material
- external materials must be ingested into the asset library before use

## Workflow

Execute in this order:

1. Normalize the request into a structured brief.
2. Verify that the source video is lawful and usable.
3. Extract transcript, scenes, and basic story structure.
4. Generate a commentary script from the source video.
5. Rewrite the script into a TTS-friendly narration draft.
6. Search supporting assets only if needed:
   - internal library first
   - Pexels for image fallback
   - internal BGM first
   - Freesound as formal external BGM fallback
7. Ingest all external assets as `candidate` entries.
8. Let the user approve or reject candidate assets when they materially affect the final output.
9. Generate Chinese narration.
10. Assemble a reviewable draft video.
11. Return the draft package and the next review actions.

## Asset rule

External assets must always follow:

`discover -> ingest -> candidate -> approve -> use`

Do not jump from discovery straight to final export.

Priority order:

- internal library first
- external libraries as fallback

## Chinese narration rule

Chinese voice quality is a core part of this skill.

Before TTS, prefer:

- pronunciation dictionary correction
- polyphone disambiguation
- person and place name normalization
- sentence splitting for speech
- pause cleanup
- emphasis cleanup

If a line reads well as text but sounds wrong in audio, rewrite it for speech.

## Output expectation

The target output is a reviewable draft package.

Preferred outputs:

- structured brief
- commentary script
- narration draft
- candidate or selected asset IDs
- voice profile used
- draft video path or task ID
- missing approvals or next actions

## Stop conditions

Do not fabricate these:

- source video
- asset approval
- final export readiness

If one of them is missing, stop clearly at that boundary and return the next prerequisite.

## Capability growth rule

When the same issue repeats, standardize it into this skill.

Typical growth areas:

- narration style profiles
- pronunciation dictionaries
- asset ingestion helpers
- candidate approval flow
- commentary assembly presets
