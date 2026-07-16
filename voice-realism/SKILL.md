---
name: fal-voice-realism
description: Create, run, improve, or diagnose natural spoken media with fal.ai video, TTS, voiceover, avatar, and lip-sync models while preserving dialogue, language, speaker identity, and creative constraints. Use when someone asks fal to generate voiced audio or video, make speech less robotic, fit dialogue to a clip, troubleshoot a voiced render, or build an authorized voice or avatar workflow. When the user requests media output, execute the generation, wait for it, download it, and return the artifact instead of returning an internal prompt. Do not use for silent or visual-only work, transcript editing or translation alone, or merely because text contains dialogue.
---

# fal Voice Realism

Create and deliver natural spoken media without silently rewriting the user's
concept. Treat the performance prompt, synthesis text, and API payload as
internal implementation details unless the user explicitly asks to see them.

Load references only when needed:

- `references/execution.md` - required end-to-end fal generation procedure
- `references/model-guidance.md` - versioned model capabilities and syntax
- `references/diagnostics.md` - symptom-based render and post-production checks
- `references/examples.md` - modality-specific behavior and output patterns

## Determine the requested outcome

Classify intent before doing any prompt work:

- **Generation:** The user asks to create, make, generate, render, run, or
  deliver audio, video, speech, a voiceover, or an avatar result. Execute fal,
  wait for completion, download the media, and return the artifact. Do not stop
  after drafting a prompt, payload, plan, or command.
- **Prompt or script only:** The user explicitly asks for a prompt, synthesis
  text, script, brief, or rewrite and does not request rendered media. Return
  that requested text without running generation.
- **Diagnosis:** The user supplies a render or describes a failed result. Inspect
  the supplied media when possible, identify the primary symptom, and propose
  or execute a controlled regeneration according to the user's request.
- **Advice or planning:** The user asks how something works or what to choose.
  Answer the question without treating it as authorization for a paid run.

An imperative to generate media is sufficient authorization for one normal
generation within the stated scope. Ask before creating extra paid variants or
changing a locked constraint. Never reinterpret a generation request as a
prompt-only request merely because the chosen model accepts a prompt.

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

## Choose the production route

- **On-camera native-audio video:** Generate picture and sound together;
  coordinate visible action, delivery, dialogue, ambience, and lip-sync-friendly
  staging.
- **Voiceover or narration:** Generate an audio track with directed timing and
  acoustic perspective; omit lip-sync and facial-performance instructions.
- **TTS:** Put only supported tags, punctuation, pronunciation guidance, and
  spoken text in the verified synthesis field, then generate and download the
  audio.
- **Avatar or separate lip-sync:** Approve and lock the final voice track first,
  then pass that exact audio to a verified avatar or lip-sync endpoint. Do not
  let the downstream step rewrite or regenerate the voice.
- **Existing render diagnosis:** Inspect or listen to the supplied output first;
  identify the audible or visible symptom before changing one variable.

For generation, discover a current endpoint when none is named. For a
prompt-only request with no target model, keep the result model-agnostic. Ask a
question only when the missing answer changes a locked constraint, makes the
request unsafe, or prevents a valid run.

## Resolve inputs

Collect only information that changes the result:

- requested deliverable and whether generation or text-only output is wanted;
- target model, version, interface, and native-audio or TTS mode;
- exact spoken lines, language, speakers, and pronunciation-sensitive terms;
- speaker count, turn order, overlap, and interruption requirements;
- clip duration and required visual action during speech;
- intended subtext, energy, intimacy, and recording perspective;
- authorized voice, character, image, audio, or video references;
- approved voice audio when an avatar or separate lip-sync step is planned;
- requested file format and destination;
- attached media and the observed failure, when diagnosing a render.

## Build the performance input

1. Restate the intended spoken outcome internally in one sentence.
2. Mark locked constraints and separate spoken text from unspoken direction.
3. Read `references/model-guidance.md` when a model is named. Treat live fal
   endpoint metadata and schema as authoritative for execution.
4. Build a minimal performance plan from:
   - intent and subtext;
   - energy and volume;
   - pace, emphasis, and pauses;
   - at most one or two context-supported nonverbal cues;
   - acoustic perspective and the relationship between dialogue, ambience, and
     music.
5. Check fit using speech, pauses, breaths, and required visual actions. Treat
   word-rate math as an estimate, not a language-independent rule. If locked
   words cannot fit naturally in the locked duration, do not spend on a known
   failure. Explain the conflict and ask the user to authorize either a longer
   duration or a shorter line.
6. Compose only fields supported by the verified route:
   - For native-audio video, describe action and delivery outside clearly
     delimited dialogue. Change framing only when it is not locked.
   - For voiceover, specify recording distance and scene-consistent acoustics
     without visible performance instructions.
   - For TTS, keep unsupported prose out of the synthesis field and use only
     documented controls.
   - For an avatar or lip-sync pass, lock the approved transcript and audio
     timing before animation.
   - For diagnosis, read `references/diagnostics.md` and change one variable at
     a time.
7. Verify that words, language, speaker order, framing, identity authorization,
   and requested format remain intact before execution or delivery.

## Execute fal generation

For every generation request, read and follow `references/execution.md`.
Discover rather than invent endpoint IDs, verify the exact endpoint, inspect its
live schema, map only supported inputs, upload local source assets when needed,
run through `genmedia`, poll long jobs to a terminal state, and download the
returned media.

Use fal support routing as a helper for model discovery or product facts, then
resume this workflow and execute the generation. A handoff, endpoint suggestion,
prompt, or CLI command is not completion when the user requested media.

After generation, inspect the output when the available tools support the media
type. Confirm at minimum that a non-empty artifact was downloaded in the
requested format. If a completed result is creatively poor, return it with one
brief caveat or ask before spending on another take. Automatically retry only a
failed preflight or clearly non-billable technical submission; do not silently
purchase multiple variants.

## Return the requested deliverable

For a generation request, make the downloaded artifact the primary result. If
the interface can render or attach it, do so. Use the verified media URL only as
a fallback when the environment cannot persist the download, and state that
limitation. Keep text to one short status line unless a material caveat exists.
Include the endpoint or request ID only when it helps trace or recover the job.

```text
Generated: [attachment or downloaded artifact path; verified URL only as a fallback]
```

Do not expose the internal prompt, synthesis field, payload, or command unless
the user asks for it. On failure, give the exact blocker and the request ID if
one exists; never present a draft prompt as if generation succeeded.

For an explicit prompt-only request, return only the requested prompt or script
plus a material assumption or constraint conflict when necessary. For a
diagnosis-only request, return the observed symptom and one controlled next
test.

## Boundaries

- Do not promise that prompting will remove all synthetic artifacts.
- Do not claim a success percentage without representative testing.
- Do not prescribe fixed EQ, reverb, noise, or voice-morpher values without
  hearing the source and defining the measurement reference.
- When no audio is available, do not provide numeric EQ, reverb, or noise
  settings even as a provisional starting point. Request the render or give one
  non-destructive comparison.
- Do not degrade intentionally clean studio speech merely to make it imperfect.
- Do not imitate or clone a real person's voice without authorization.
- When a voice ID or reference represents a real person, require the user to
  state that they have permission to use or clone it. A public recording, an
  employment relationship, or an internal-use claim is not authorization. If
  permission is absent, stop that route or use a non-imitative licensed voice.
- Do not remove or contradict required disclosure or watermark instructions.
- Do not invent endpoint IDs, schema fields, capabilities, language support,
  prices, job status, or artifact URLs.
- Do not launch extra paid takes, variants, or downstream stages beyond the
  user's requested deliverable without authorization.
- Prefer upstream fixes such as copy, voice choice, pronunciation, pacing, and
  generation settings before destructive post-processing.
- Compare variants with the same model, version, voice, settings, and source;
  change one variable per test and judge naturalness, intelligibility, timing,
  and lip-sync separately.

Finish a generation request with generated media or a specific execution
blocker, never with only a prompt.
