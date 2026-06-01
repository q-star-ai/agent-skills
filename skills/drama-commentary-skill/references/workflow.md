# Workflow

Use this workflow when handling a `剧情解说` request.

The goal is to produce a reviewable draft package from a lawful source video.

## 1. Normalize the brief

Turn the user request into a structured brief:

- title
- source video path or upload URL
- target duration
- commentary style profile
- language
- whether candidate images are needed
- whether candidate BGM is needed

If style is unclear, choose the closest style from [style-profiles.md](style-profiles.md).

## 2. Verify the source video

Check that the source video is one of:

- local file from the user
- user upload
- lawful authorized link

Do not proceed if the workflow depends on downloading an unauthorized full film.

## 3. Extract source structure

Prefer a structured result from `video-understanding-skill`.

From the source video or the upstream understanding package, produce:

- transcript or subtitles
- scene boundaries
- rough plot beats
- major characters
- likely climax and reversal moments

This step is for structure first, polish later.

## 4. Build the story skeleton

When an upstream understanding package exists, consume it in this priority:

1. `highlights`
2. `story`
3. `scenes`
4. `transcript.segments`
5. `uncertainties`

Condense the plot into:

- hook
- setup
- conflict escalation
- major turn
- climax
- ending or emotional close

Do not summarize scene by scene blindly.

The script must feel like guided storytelling, not a raw timeline dump.

## 5. Draft the commentary script

Generate the first commentary script using the selected style profile.

Priorities:

- first 8 seconds must hook
- keep plot progression clear
- choose what to omit
- preserve the emotional or suspense line
- prefer upstream `highlights` for hook / reversal / climax material

Aim for readable structure before voice polish.

## 6. Rewrite for Chinese narration

Convert the script into a speech-friendly draft.

Apply:

- sentence splitting
- polyphone disambiguation
- person and place name normalization
- number and date normalization
- pause cleanup
- emphasis cleanup

If a sentence looks elegant but sounds wrong when read aloud, rewrite it.

## 7. Gather supporting assets

Only gather supporting assets if they are useful.

Priority:

1. internal library
2. fallback image sources
3. fallback BGM sources

Current fallback path:

- images: Pexels
- BGM: internal library first, then Freesound as the formal external source

## 8. Ingest external assets

External materials must be turned into asset records before use.

Required state:

- `candidate`

Do not use newly discovered external assets directly in final export.

Expected record types:

- candidate images
- candidate BGM

For final consumption, the commentary layer should only trust:

- `final_public_url`
- `final_qiniu_key`
- `status`
- `upload_status`
- `license`

## 9. Confirm user selection when needed

If the selected images or BGM materially shape the output, let the user choose.

Typical cases:

- cover image
- main BGM
- ending BGM
- strong visual inserts

If asset choice does not matter much for the current draft, use approved internal defaults.

For production-safe selection:

- only consume `status=approved`
- only consume `upload_status=done` unless the record is explicitly legacy-safe
- for BGM, prefer `cc0` and `cc-by`
- do not consume `cc-by-nc` or unclear licenses

## 10. Generate voice

Run the narration through the Chinese voice pipeline.

Always treat voice quality as part of the creative result, not a final mechanical step.

Check for:

- wrong polyphone readings
- unnatural pauses
- mismatched energy
- poor emotional fit

## 11. Assemble the draft video

Create a reviewable draft package with:

- narration audio
- source-video-based scene selection
- approved supporting assets
- BGM
- subtitles if available

The goal is a draft the user can react to quickly.

Do not optimize for perfect edit polish in the first pass.

## 12. Return the package

Return:

- structured brief
- selected style profile
- commentary script
- narration draft
- candidate and selected asset IDs
- draft video path or task ID
- next actions

## Default fallback rule

If one part is blocked, do not collapse the whole workflow.

Fallback examples:

- no external assets yet -> continue with internal defaults
- no final BGM approval yet -> produce a draft with placeholder BGM
- no final voice chosen yet -> produce one default voice pass

Only stop when the missing item makes the next step invalid.

## Quality bar

A usable first draft should satisfy:

- clear hook
- coherent plot line
- no obvious narration reading failures
- no direct use of unapproved external assets
- enough structure for the user to react quickly
