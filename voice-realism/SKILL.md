---
name: fal-voice-realism
description: Improve or diagnose natural spoken performance for fal.ai video, TTS, voiceover, avatars, and lip-sync while preserving dialogue, language, speaker identity, and creative constraints. Use when someone asks to make speech less robotic, rewrite a prompt where voice quality is material, fit dialogue to a clip, troubleshoot a voiced render, or prepare a voice-performance brief for fal generation. Do not use for silent or visual-only work, transcript editing or translation alone, or merely because text contains dialogue.
---

# fal Voice Realism

Direct spoken performance without silently rewriting the user's concept. Produce
the smallest useful prompt, script, or diagnosis for the requested modality.

Load references only when needed:

- `references/model-guidance.md` - versioned model capabilities and syntax
- `references/diagnostics.md` - symptom-based render and post-production checks
- `references/examples.md` - modality-specific answer patterns

## Preserve first

Treat these as locked unless the user explicitly permits changes:

- spoken wording and meaning;
- language, pronunciation intent, and speaker assignment;
- speaker identity and authorized voice references;
- duration, shot, framing, and source assets;
- requested model, output format, creative tone, and disclosure requirements.

Do not infer an accent, age, disability, health condition, or a trait such as a
"smoker's voice" from appearance or demographics. Do not add fillers, stutters,
whispers, breaths, laughs, or scene changes merely to hide synthesis artifacts.
When a useful improvement conflicts with a locked constraint, preserve the
requested version and label the improvement as an optional alternative.

## Fast routing

Choose one primary mode before rewriting:

- **On-camera native-audio video:** coordinate visible action, delivery,
  dialogue, room sound, and lip-sync-friendly staging.
- **Voiceover or narration:** direct voice, timing, and acoustic perspective;
  omit lip-sync and facial-performance instructions.
- **TTS:** return only supported tags, punctuation, pronunciation guidance, and
  spoken text for the synthesis field. Keep visual stage directions separate.
- **Avatar or separate lip-sync:** approve and lock the final voice track first;
  treat lip-sync as a downstream alignment step, not a chance to rewrite or
  regenerate the voice.
- **Existing render diagnosis:** inspect or listen to the supplied output first;
  identify the audible or visible symptom before recommending a change.

If the target model or version is unknown, produce a model-agnostic result.
Ask a question only when the missing answer would materially change a
paste-ready result. Otherwise state the assumption briefly and continue.

## Inputs to resolve

Collect only information that changes the result:

- target model, version, interface, and native-audio or TTS mode;
- exact spoken lines, language, speakers, and pronunciation-sensitive terms;
- speaker count, turn order, overlap, and interruption requirements;
- clip duration and required visual action during speech;
- intended subtext, energy, intimacy, and recording perspective;
- authorized voice or character references;
- approved voice audio when an avatar or separate lip-sync step is planned;
- requested output format and whether post-production help is wanted;
- attached audio or video and the observed failure, when diagnosing a render.

## Workflow

1. Restate the intended spoken outcome in one sentence.
2. Mark locked constraints and separate spoken text from unspoken direction.
3. Read `references/model-guidance.md` when a model is named. Verify volatile
   capability, language, duration, and syntax against the current endpoint or
   official documentation before presenting them as facts.
4. Build a minimal performance plan from:
   - intent and subtext;
   - energy and volume;
   - pace, emphasis, and pauses;
   - at most one or two context-supported nonverbal cues;
   - acoustic perspective and the relationship between dialogue, ambience, and
     music.
5. Check fit using speech, pauses, breaths, and required visual actions. Treat
   word-rate math as an estimate, not a language-independent rule. If the line
   does not fit, keep the original and offer either a clearly labeled shorter
   version or a longer duration.
   Do not pretend mutually locked constraints are compatible. Do not force fit
   by starting on the first frame, accelerating unnaturally, removing all
   pauses, overlapping speakers, or asserting that every line will fit. Lead
   with the timing conflict and request authorization for one of the two
   alternatives before producing a paste-ready prompt that claims success.
6. Compose for the selected mode:
   - For on-camera video, describe action and delivery outside clearly delimited
     dialogue. Suggest a tighter or steadier shot only when framing is not
     locked, and explain the tradeoff.
   - For voiceover, specify recording distance and scene-consistent acoustics
     without adding visible performance instructions.
   - For TTS, keep unsupported prose out of the synthesis field and use only
     current, documented controls.
   - For an avatar or separate lip-sync pass, lock the approved transcript and
     audio timing before animation. Do not let the downstream step regenerate
     or paraphrase the voice.
   - For a render diagnosis, read `references/diagnostics.md` and change one
     variable at a time.
7. Verify that the final spoken words, language, speaker order, framing, and
   requested format remain intact. Remove invented identity traits and
   unsupported model claims.

## fal handoff

Keep this skill responsible for dialogue and voice performance. When the user
also requests model selection, pricing, endpoint discovery, or generation, use
the fal support routing workflow for that part. Before execution, verify the
live endpoint, schema, native-audio mode, supported duration, language, and
required inputs. Never invent an endpoint ID or assume that a model-family name
maps to one stable schema.

When an endpoint is known, verify it before running:

```bash
genmedia models --endpoint_id <endpoint_id> --json
genmedia schema <endpoint_id> --json
genmedia pricing <endpoint_id> --json
```

Check pricing only when cost matters. Hand off the objective, locked transcript,
language and pronunciations, speaker order and authorization, timing, source
assets, compact performance cues, verified schema fields, and acceptance gates.

## Answer format

Honor the user's requested language and output shape. If none is specified,
return only the sections that apply:

```text
Prompt or script: [paste-ready result]
Assumptions: [only material assumptions]
Optional alternative: [only when a locked constraint creates a tradeoff]
Diagnosis: [only when an output was supplied or a failure was described]
```

Do not append a mandatory explanation or post-processing checklist to a
prompt-only request.

## Boundaries

- Do not promise that a prompt will remove all synthetic artifacts.
- Do not claim a success percentage without representative testing.
- Do not prescribe fixed EQ, reverb, noise, or voice-morpher values without
  hearing the source and defining the measurement reference.
- When no audio is available, do not provide numeric EQ, reverb, or noise
  settings even as a provisional starting point. Give one non-destructive
  comparison or request the render instead.
- Do not degrade intentionally clean studio speech merely to make it imperfect.
- Do not imitate or clone a real person's voice without authorization.
- Do not remove or contradict required disclosure or watermark instructions.
- Prefer upstream fixes such as copy, voice choice, pronunciation, pacing, and
  generation settings before destructive post-processing.
- Compare variants with the same model, version, voice, settings, and source;
  change one variable per test and judge naturalness, intelligibility, timing,
  and lip-sync separately.

Always leave the user with a usable result or one specific next test.
