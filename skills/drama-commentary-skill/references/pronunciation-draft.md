# Pronunciation Draft

Use this reference before Chinese TTS generation.

The purpose is to reduce obvious reading failures in commentary voiceover.

Focus on:

- polyphones
- person and place names
- movie and drama titles
- numbers and dates
- pause placement

## Core rule

Do not send the raw script directly into TTS if it still contains likely pronunciation ambiguity.

First convert the script into a speech-safe draft.

## 1. Polyphone handling

Chinese commentary scripts often fail on polyphones.

Typical risk types:

- common words that change by context
- historical names
- role titles
- mixed written and spoken phrasing

### Handling rule

When a word is likely ambiguous:

1. prefer rewriting the sentence to remove ambiguity
2. if rewriting hurts style, annotate or replace with a safer equivalent form
3. keep a reusable dictionary for repeated names and terms

### Rewrite examples

- `角色` -> if needed, rewrite to `人物角色`
- `还债` -> keep as a spoken phrase that makes the reading obvious
- `长大` -> keep the surrounding context explicit
- `重逢` / `重庆` / `重要` -> avoid isolated short phrases that confuse the engine

The principle is not “preserve the exact original wording at all cost”.
The principle is “make it sound right in voice”.

## 2. Person and place names

Names are high-risk and should be normalized before TTS.

### Required treatment

- normalize uncommon historical names
- normalize transliterated foreign names
- normalize fictional names used repeatedly in one script
- keep one stable form throughout the full draft

### Rule

If a name appears 3 or more times, lock one canonical spoken form and reuse it.

Avoid:

- switching between translated and untranslated forms
- one paragraph using surname only and another using full name if that changes TTS behavior

## 3. Title handling

Film and drama titles often sound awkward in TTS when punctuation is left untouched.

### Rule

- remove unnecessary decorative punctuation
- keep title wording stable
- if a title is hard to read aloud, separate title mention from plot sentence

Example pattern:

- not: `而《某某：终局之战》真正厉害的地方在于……`
- better: `《某某终局之战》真正厉害的地方，在于……`

The point is smoother spoken rhythm.

## 4. Numbers and dates

Numbers are another common failure point.

### Normalize these consistently

- years
- money
- rankings
- episode numbers
- timestamps

### Rules

- years should read naturally in spoken Chinese
- large numbers should be grouped for listening clarity
- episode references should be explicit
- avoid compressed symbolic forms when a spoken form is safer

Examples:

- `2024年` -> keep in a form the TTS reads naturally
- `第12集` -> explicit episode form
- `3分钟` -> explicit spoken duration form
- `80万点赞` -> keep as a spoken-count phrase, not a bare number cluster

## 5. English and mixed-language text

Mixed Chinese-English scripts often break flow badly.

### Rule

- do not leave product names, acronyms, or English fragments floating in long Chinese sentences
- either localize them into the spoken Chinese version
- or isolate them with pauses

If a term is famous in English and must stay in English, reduce surrounding sentence complexity.

## 6. Pause strategy

Pause placement matters as much as pronunciation.

### Add pauses for

- reversals
- emotional turns
- name reveals
- conclusion sentences
- hook endings

### Remove pauses from

- overly fragmented short clauses
- places where TTS already inserts a break naturally
- repeated comma chains that make speech choppy

The goal is guided rhythm, not punctuation spam.

## 7. Sentence rewrite rule

A sentence can be rewritten if it improves any of these:

- pronunciation accuracy
- emotional delivery
- clarity in listening
- rhythm

This matters more than preserving every written nuance.

## 8. Minimum pre-TTS checklist

Before sending script into Chinese TTS, check:

- polyphones reduced or rewritten
- names normalized
- titles normalized
- numbers and dates made speakable
- mixed-language fragments simplified
- pauses added only where useful

## 9. Output form

The preferred result is not just “final script”.

It should be:

- `display_script`: for on-screen review
- `tts_script`: for voice generation

These may differ slightly.

That difference is acceptable and often necessary.
